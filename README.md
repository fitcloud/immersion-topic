# AI Workshop Tools Claude Code Marketplace

Version: v1.0.0

AWS Immersion Day 및 AI 워크숍 주제를 객관적으로 조사, 평가, 선정하기 위한 Claude Code 플러그인 마켓플레이스입니다.

## Included Plugin

- `immersion-day-topic-selection-plugin`
  - 명시 호출형 Immersion Day 주제 선정 Skill
  - AWS Immersion Day 후보 주제 선정
  - 기존 FitCloud 교육 이력 확인
  - AWS Knowledge Base MCP 및 AWS 공식 자료 기반 조사
  - AI Engineer YouTube 및 Lenny's Podcast 기반 외부 트렌드 확인
  - 회사 맥락과 고객 페르소나 반영
  - 객관 평가표와 산정 이유 생성
  - 투표용 HTML 생성

## 변경사항

- `SKILL.md`를 핵심 워크플로우 중심으로 줄이고, 상세 자료는 `references/`와 `assets/`로 분리했습니다.
- 평가 점수별 1/3/5 기준과 후보별 점수 산정 근거를 반드시 남기도록 강화했습니다.
- `company-context.yaml`에 FitCloud/Saltware 공개 정보와 고객 믹스, 산업군, 고객 페르소나를 반영했습니다.
- 기존 진행 교육은 `https://workshop.fitcloud.co.kr/immersion-day`와 각 상세 페이지를 우선 확인하도록 추가했습니다.
- AWS What’s New는 AWS Knowledge Base MCP에서 우선 조회하도록 명시했습니다.
- AWS Events는 세부 근거가 아니라 상위 메시지와 교육 포맷 확인용으로 정리했습니다.
- AWS Builder Center Workshops는 Discover 탭에서 AI 관련 키워드와 필터를 사용해 확인하도록 정리했습니다.
- AI Engineer YouTube(`https://www.youtube.com/@aiDotEngineer/videos`)와 Lenny's Podcast(`https://www.youtube.com/@LennysPodcast`)를 외부 영상 트렌드 우선 소스로 지정했습니다.
- HTML 결과물에는 점수뿐 아니라 핵심 산정 이유와 회사 적합성 근거를 함께 표시하도록 정리했습니다.

## 저장소 구조

GitHub repository root 기준 구조입니다.

```text
.claude-plugin/
  marketplace.json
README.md
plugins/
  immersion-day-topic-selection-plugin/
    .claude-plugin/
      plugin.json
    skills/
      immersion-day-topic-selection/
        SKILL.md
        data/
          company-context.yaml
        references/
          evaluation-rubric.md
          research-sources.md
          output-format.md
        assets/
          voting-template.html
```

## 설치

상대 경로 플러그인을 사용하므로 marketplace는 GitHub 저장소 방식으로 추가해야 합니다.

현재 저장소 기준:

```bash
/plugin marketplace add fitcloud/immersion-topic
```

저장소 이름을 변경했다면 실제 GitHub 저장소 경로로 바꿔 실행하세요.

```bash
/plugin marketplace add <github-org>/<repo-name>
```

`marketplace.json` 파일의 직접 URL을 추가하는 방식은 상대 경로 플러그인 설치에 적합하지 않습니다.

## 권장 MCP

정확한 AWS 공식 근거 확인을 위해 AWS Knowledge MCP Server를 사용합니다.

- 용도: AWS Documentation, Blog, What's New, Builder Center 등 읽기 전용 AWS 지식 검색
- 사용 위치: 후보 주제별 AWS 공식 근거 조사, 서비스 업데이트 확인, 실습 가능성 검토
- 없을 경우: AWS 공식 웹 문서를 fallback으로 사용하며 결과에 `AWS official web fallback`으로 표시

이 플러그인은 plugin-provided MCP 설정으로 AWS Knowledge MCP Server를 포함합니다.

```text
plugins/immersion-day-topic-selection-plugin/.mcp.json
```

설치 후 Claude Code에서 `/reload-plugins`를 실행하고 `/mcp`에서 `aws-knowledge` 서버가 연결되어 있는지 확인하세요.

수동 등록이 필요하거나 사용자 범위로 별도 등록하려면 [docs/aws-knowledge-mcp-setup.md](docs/aws-knowledge-mcp-setup.md)를 참고하세요.

## Skill 호출 방법

이 플러그인의 skill은 명시적 호출이 필요합니다.

```text
/immersion-day-topic-selection-plugin:immersion-day-topic-selection <요청 내용>
```

## 사용 예시

```text
/immersion-day-topic-selection-plugin:immersion-day-topic-selection 이머전데이 주제 선정해보자.
```

```text
/immersion-day-topic-selection-plugin:immersion-day-topic-selection 7월 이머전데이 주제 3개 추천해줘.
지난번 AgentCore Gateway, Datadog LLM Observability는 제외하고
반나절 실습형으로 보고, 투표용 HTML로 만들어줘.
```

## 검증 방법

마켓플레이스 구조 검증:

```bash
claude plugin validate .
```

플러그인 구조 검증:

```bash
claude plugin validate ./plugins/immersion-day-topic-selection-plugin
```

설치 후 Claude Code에서 확인:

```text
/reload-plugins
/mcp
```

`/mcp`에서 `aws-knowledge`가 연결되어 있는지 확인합니다.

## 운영 메모

- 기존 교육 이력은 FitCloud Workshop 사이트를 우선 확인합니다.
- `data/company-context.yaml`은 회사 전략, 고객군, 보유 데모, 영업 방향이 바뀌면 업데이트하세요.

## 지원

문의나 개선 요청은 GitHub Issue 또는 FitCloud 내부 담당 채널로 남겨주세요.

## 라이선스

현재 배포 목적은 FitCloud 내부 공통 사용입니다. 외부 공개 또는 오픈소스 배포 전 라이선스를 확정하세요.
