# Contributing

이 저장소는 FitCloud 내부 공통 사용을 우선합니다.

## 수정 원칙

- `SKILL.md`에는 핵심 workflow만 유지합니다.
- 긴 조사 규칙은 `references/research-sources.md`에 둡니다.
- 평가 기준은 `references/evaluation-rubric.md`에 둡니다.
- 출력 형식은 `references/output-format.md`에 둡니다.
- 회사 정보는 `data/company-context.yaml`에 둡니다.
- 투표 HTML 템플릿은 `assets/voting-template.html`에 둡니다.

## 검증

수정 후 아래 명령을 실행합니다.

```bash
claude plugin validate .
claude plugin validate ./plugins/immersion-day-topic-selection-plugin
```

설치 후 Claude Code에서 다음을 확인합니다.

```text
/reload-plugins
/mcp
```

`aws-knowledge` MCP 서버가 연결되어 있는지 확인합니다.

## 릴리스

- `README.md`의 version을 업데이트합니다.
- `.claude-plugin/marketplace.json`의 `metadata.version`과 plugin `version`을 맞춥니다.
- `plugins/immersion-day-topic-selection-plugin/.claude-plugin/plugin.json`의 `version`을 맞춥니다.
- `CHANGELOG.md`에 변경사항을 추가합니다.
