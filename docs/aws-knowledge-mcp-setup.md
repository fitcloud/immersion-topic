# AWS Knowledge MCP Server Setup

이 문서는 `immersion-day-topic-selection-plugin`에서 AWS 공식 근거 조사를 더 일관되게 수행하기 위한 AWS Knowledge MCP Server 설정 방법을 정리합니다.

## 왜 필요한가

이 플러그인은 AWS Immersion Day 주제 선정 시 AWS 공식 근거를 우선 확인합니다.

AWS Knowledge MCP Server가 등록되어 있으면 다음 자료를 MCP 기반으로 조회할 수 있습니다.

- AWS Documentation
- AWS API references
- AWS What's New
- AWS Blog posts
- Builder Center content
- architecture references
- Well-Architected guidance

AWS Knowledge MCP Server가 없는 환경에서는 플러그인이 AWS 공식 웹 문서를 fallback으로 사용하고, 결과에 `AWS official web fallback`으로 표시합니다.

## 전제

- Claude Code에서 MCP remote HTTP server를 사용할 수 있어야 합니다.
- 네트워크에서 `https://knowledge-mcp.global.api.aws`에 접근할 수 있어야 합니다.
- AWS Knowledge MCP Server는 AWS 계정이나 AWS credentials 없이 사용할 수 있습니다.
- 사용량은 AWS 측 rate limit의 영향을 받을 수 있습니다.

## 기본 방식: 플러그인 제공 MCP

이 플러그인은 plugin-provided MCP 설정을 포함합니다.

```text
plugins/immersion-day-topic-selection-plugin/.mcp.json
```

내용은 다음과 같습니다.

```json
{
  "mcpServers": {
    "aws-knowledge": {
      "type": "http",
      "url": "https://knowledge-mcp.global.api.aws"
    }
  }
}
```

플러그인을 설치한 뒤 Claude Code에서 다음을 실행합니다.

```text
/reload-plugins
/mcp
```

`/mcp` 목록에서 `aws-knowledge`가 연결되어 있는지 확인합니다.

## 선택 방식: Claude Code CLI로 사용자 범위 등록

개인 사용자 범위에 등록하는 것을 권장합니다.

```bash
claude mcp add --transport http aws-knowledge --scope user https://knowledge-mcp.global.api.aws
```

프로젝트에 공유 설정으로 등록하려면 다음을 사용합니다.

```bash
claude mcp add --transport http aws-knowledge --scope project https://knowledge-mcp.global.api.aws
```

프로젝트 범위로 등록하면 `.mcp.json`이 생성될 수 있습니다. 팀 저장소에 포함하기 전에 회사 보안 정책에 맞는지 확인하세요.

## 선택 방식: 프로젝트 `.mcp.json`

프로젝트 루트에 직접 `.mcp.json`을 작성하는 경우:

```json
{
  "mcpServers": {
    "aws-knowledge": {
      "type": "http",
      "url": "https://knowledge-mcp.global.api.aws"
    }
  }
}
```

Claude Code는 프로젝트 범위 MCP 서버를 처음 사용할 때 승인을 요청할 수 있습니다.

## 등록 확인

터미널에서:

```bash
claude mcp list
claude mcp get aws-knowledge
```

Claude Code 세션 안에서:

```text
/mcp
```

`aws-knowledge` 서버가 연결되어 있고 tools/resources가 표시되는지 확인합니다.

## 플러그인 사용 시 기대 동작

`immersion-day-topic-selection` skill은 AWS 근거 조사 단계에서 다음 순서를 따릅니다.

1. AWS Knowledge MCP Server 사용 가능 여부 확인
2. 가능하면 AWS What's New, docs, blog, service context를 MCP로 먼저 조회
3. 후보별로 MCP 근거 또는 MCP 미사용 사유 기록
4. MCP가 없거나 부족하면 AWS 공식 웹 문서 fallback 사용
5. MCP를 실제로 조회하지 않았으면 사용했다고 쓰지 않음

결과에는 다음 중 하나가 표시되어야 합니다.

```text
AWS Knowledge MCP: used
```

또는:

```text
AWS Knowledge MCP was not available in this session.
AWS evidence type: AWS official web fallback
```

## 문제 해결

### 서버가 목록에 보이지 않음

```bash
claude mcp list
```

출력에 `aws-knowledge`가 없으면 등록 명령을 다시 실행합니다.

### `/mcp`에서 연결 실패로 보임

- 회사 네트워크에서 `https://knowledge-mcp.global.api.aws` 접근이 가능한지 확인합니다.
- 프록시/VPN 정책이 remote MCP 연결을 막고 있지 않은지 확인합니다.
- Claude Code를 재시작하거나 `/reload-plugins`를 실행한 뒤 다시 확인합니다.

### MCP를 등록했는데 결과가 fallback으로 나옴

- 해당 Claude Code 세션에서 `/mcp`로 서버가 연결되어 있는지 확인합니다.
- skill 실행 결과에 MCP 미사용 사유가 적혀 있는지 확인합니다.
- MCP가 연결되어 있어도 특정 질의 결과가 부족하면 AWS 공식 웹 fallback이 함께 사용될 수 있습니다.

## 참고 문서

- AWS Knowledge MCP Server: https://awslabs.github.io/mcp/servers/aws-knowledge-mcp-server/
- AWS MCP Servers GitHub: https://github.com/awslabs/mcp
- Claude Code MCP: https://code.claude.com/docs/en/mcp
