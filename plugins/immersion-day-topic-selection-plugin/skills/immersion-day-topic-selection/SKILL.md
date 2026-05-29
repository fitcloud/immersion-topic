---
description: AWS Immersion Day 주제를 조사, 평가, 선정하고 투표용 HTML을 생성합니다.
disable-model-invocation: true
---

# Immersion Day Topic Selection Skill

## 목적

이 Skill은 AWS Immersion Day, 고객 워크숍, 사내 Knowledge Sharing, 파트너 교육, PoC 발굴, 서비스 오퍼링 기획 주제를 선정할 때 사용한다.

결과는 단순 아이디어 목록이 아니어야 한다. 반드시 다음을 포함한다.

- 올해 FitCloud Immersion Day 주제 중복/유사성 확인
- 회사 맥락과 서비스 오퍼링 적합성
- AWS 공식 근거. 가능하면 AWS Knowledge Base MCP를 먼저 사용
- 외부 YouTube/AI Engineering 근거. 가능하면 AI Engineer와 Lenny's Podcast를 우선 확인
- 객관 평가 기준과 점수 산정 이유
- 최종 추천 주제 3개
- 서비스 오퍼링 가능성
- 요청 시 투표용 요약 또는 HTML

## 사전 조건

이 Skill은 다음 환경에서 가장 잘 동작한다.

- AWS 문서, 블로그, What's New, 서비스 맥락 확인용 AWS Knowledge Base MCP server (`aws-knowledge`)
- FitCloud Workshop 페이지, YouTube, 외부 트렌드 소스를 확인할 수 있는 web search/browser 기능

AWS Knowledge Base MCP를 사용할 수 없으면 AWS 공식 웹 문서를 fallback으로 사용하고, 결과에 fallback 사용 사실을 명확히 적는다.

## Progressive Loading

필요한 파일만 로드한다.

시작 시 항상 로드한다.

- `data/company-context.yaml`

단계별로 필요할 때 로드한다.

- 조사 단계: `references/research-sources.md`
- 평가 단계: `references/evaluation-rubric.md`
- 최종 답변 또는 HTML 단계: `references/output-format.md`
- HTML 요청 시: `assets/voting-template.html`

참조 파일 내용을 답변에 그대로 붙여 넣지 말고, 작업 기준으로만 사용한다.

## 필수 입력

조사 전에 가능하면 아래 입력을 확인한다. 일부가 없어도 진행할 수 있지만, 막히는 정보만 짧게 질문한다.

조사 전에 필요한 입력:

1. 교육 시간
   - 예: 1시간, 2시간, 3-4시간, 5-7시간, 여러 회차, 미정
   - 시간이 없으면 먼저 질문한다. 시간은 주제 범위와 실습 가능성을 크게 바꾼다.

2. 기존 또는 제외 주제
   - 먼저 올해 FitCloud Immersion Day 이력을 자동 확인한다.
   - 사용자가 직접 준 제외 주제도 반영한다.

3. 사용자가 생각 중인 후보 또는 방향
   - 사용자 후보는 1차 후보군에 포함한다.
   - 사용자가 제안했다는 이유로 가산점을 주지 않는다.

있으면 좋은 입력:

- 교육 목적
- 대상자
- 선호 AWS 서비스 또는 도메인
- 준비된 demo, code, architecture, SME
- 회사 전략, 고객군, 현재 오퍼링, 영업 pain point
- 피해야 할 주제

회사 맥락:

- `data/company-context.yaml`을 우선 사용한다.
- 사용자가 더 최신 회사 맥락을 제공하면 이번 실행에서는 사용자 입력을 우선한다.
- 회사 맥락이 부족하면 어떤 정보가 있으면 평가가 개선되는지 명확히 말한다.

## 입력 처리

### 넓은 요청

사용자가 "이머전데이 주제 선정해보자"처럼 넓게 요청하면, 조사 전에 짧게 확인한다.

```text
주제 선정을 시작하기 전에 세 가지만 확인하겠습니다.

1. 이번 Immersion Day는 몇 시간 정도인가요?
2. 이미 생각 중인 후보 주제나 관심 방향이 있나요?
3. 추가로 제외해야 할 주제가 있나요? 기존 FitCloud Immersion Day 목록은 제가 먼저 확인하겠습니다.
```

이미 답한 항목이 있으면 빠진 필수 항목만 질문한다.

### 시간이 없는 경우

교육 시간이 확인되기 전에는 외부 트렌드 조사를 시작하지 않는다.

사용자가 "미정"이라고 하면 시간 시나리오별로 평가한다.

- 1시간: executive briefing 또는 demo
- 2시간: seminar plus short demo
- 3-4시간: hands-on Immersion Day
- 5-7시간: deeper lab 또는 team exercise

### 기존 주제가 없는 경우

사용자에게 먼저 묻지 말고, 올해 FitCloud Immersion Day 이력을 먼저 확인한다.

주요 확인 URL:

- `https://workshop.fitcloud.co.kr/immersion-day`

확인 절차:

1. 목록 페이지를 연다.
2. 올해 Immersion Day 항목을 식별한다.
3. 모든 올해 항목의 상세 페이지를 연다.
4. 작년 이전 항목은 기본 확인 대상이 아니지만, 사용자가 특정 과거 주제를 제외했거나 후보와 제목, AWS 서비스, 키워드가 명확히 겹치면 해당 상세 페이지만 추가로 연다.
5. 제목, 날짜, 교육 목표, 대상, agenda, 자료 링크, AWS 서비스, 키워드를 추출한다.
6. 유사성을 High, Medium, Low로 표시한다.
7. High 유사성이거나 사용자가 명시적으로 제외한 주제만 제외 또는 하향 평가한다.

기본 범위:

- 올해 주제만 확인한다.
- 올해 필터링이 어려우면 최근 6개월 또는 최근 3-5개 Immersion Day 페이지를 확인한다.
- 작년 이전 주제는 자동 제외하지 않는다.
- AWS 서비스, 고객 문제, 실습 시나리오, 오퍼링 경로가 크게 달라졌다면 과거 주제도 재해석할 수 있다.
- 사용자가 특정 과거 주제를 제외하라고 하면 연도와 관계없이 제외 또는 하향 평가한다.
- 확인 범위를 반드시 적는다. 예: "올해 FitCloud Immersion Day 페이지를 확인했고, 상세 페이지 4개를 열었습니다."

사이트 접근이나 파싱이 불가능하면 그때 사용자에게 기존 주제를 요청한다.

### 사용자가 제공한 제외 주제

사용자가 기존 또는 제외 주제를 직접 제공하면 이번 실행에는 즉시 사용한다.

별도 파일에 저장하지 않는다. 다음 실행에서는 FitCloud Workshop 사이트를 다시 확인하고, 사용자가 새로 제공한 제외 주제만 추가 반영한다.

## Workflow

### Step 1. 필수 데이터 로드

다음을 읽는다.

- `data/company-context.yaml`

이번 실행의 동적 맥락으로 사용한다.

`company-context.yaml`에 unknown 또는 빈 값이 있으면 무엇이 부족한지 명확히 말한다.

### Step 2. 선정 목적 정의

다음을 정리한다.

- 주요 목적
- 보조 목적
- 대상자, 알려진 경우
- 시간 제약
- 회사 맥락 가정
- 피해야 할 방향

### Step 3. 이전 FitCloud Workshop 확인

FitCloud Workshop 사이트를 먼저 확인하고, 기본 범위는 올해 Immersion Day 주제로 한다.
확인 깊이와 유사성 판단 규칙은 `references/research-sources.md`를 따른다.

각 관련 상세 페이지에서 다음을 추출한다.

- 제목과 날짜
- 교육 목표
- 대상자
- agenda
- 자료 링크
- 관련 AWS 서비스
- 키워드
- 후보 주제와의 유사성

작년 이전 주제는 사용자가 명시적으로 제외하라고 하지 않는 한 자동 제외하지 않는다.

출력에는 기존 주제 처리를 반드시 포함한다.

- 제외한 주제
- 하향 평가한 주제
- 확인 범위와 열어본 상세 페이지 수
- 제외 또는 유사성 판단에 사용한 근거 URL

### Step 4. 사용자 후보 확인

외부 트렌드 조사 전에 사용자의 후보가 없으면 후보 아이디어를 질문한다.

사용자 후보는 1차 후보군에 포함하되, 다른 후보와 같은 rubric으로 평가한다.

### Step 5. AWS 및 외부 신호 조사

`references/research-sources.md`를 로드한다.

그 파일의 조사 소스 우선순위, 최소 근거 기준, fallback 규칙을 따른다.
AWS 근거를 web search로 찾기 전에 AWS Knowledge Base MCP 사용 가능 여부를 확인한다.

각 후보에 대해 다음을 기록한다.

- AWS Knowledge Base MCP 근거 또는 MCP 미사용 사유
- AWS 공식 근거
- 외부 YouTube/AI Engineering 근거
- FitCloud 이전 workshop 유사성
- 회사 맥락 적합성
- hands-on feasibility

### Step 6. 1차 후보군 구성

최종 3개로 좁히기 전에 후보 5-7개를 만든다.

각 후보에는 다음을 포함한다.

- 주제명
- 한 줄 아이디어
- 관련 AWS 서비스
- 고객 문제 가설
- hands-on scenario
- 회사 적합성 가설
- 기존 workshop 중복 위험
- 근거 자료

### Step 7. 객관 평가

`references/evaluation-rubric.md`를 로드한다.

각 후보를 1-5점으로 평가한다.

- 최신성
- 고객 문제 가설 신뢰도
- hands-on feasibility
- AWS service fit
- differentiation
- presentation feasibility
- service offering potential
- reusability
- company fit

규칙:

- 사용자 선호 가산점은 없다.
- 보정 또는 조정 컬럼을 만들지 않는다.
- 최종 점수는 객관 기준 점수의 합이다.
- 모든 기준 점수에는 산정 이유가 있어야 한다.
- 1-4점은 왜 더 높은 점수가 아닌지 설명한다.
- 5점은 5점 기준을 충족한다고 명시한다.
- 점수표 아래에 산정 이유 요약을 포함한다.

### Step 8. 서비스 오퍼링 가능성 평가

주제가 반복 가능한 유료 오퍼링이 될 수 있는지 평가한다.

기준:

- High: PoC, consulting, build, operations, governance package로 전환 가능
- Medium: 일부 고객군에는 가능하지만 customization 필요
- Low: 트렌드 교육으로는 유용하나 오퍼링 경로가 약함

다음을 설명한다.

- repeatable pattern
- likely buyer pain
- PoC conversion path
- standard AWS architecture 가능성
- security/operations/governance 확장 가능성
- industry reusability

### Step 9. 최종 3개 선정

다음을 기준으로 3개를 선정한다.

- 점수
- 올해 FitCloud workshop과 낮은 중복도
- 서로 다른 고객 문제
- 투표 비교 용이성
- stable topic 최소 1개
- trend topic 최소 1개
- offering-oriented topic 최소 1개

### Step 10. 최종 출력 생성

`references/output-format.md`를 로드한다.

최종 답변에는 다음을 포함한다.

- 목적과 제약
- 회사 맥락
- 이전 workshop 제외/유사성
- 조사 근거
- 1차 후보군
- 평가 기준
- 점수표
- 점수 산정 이유 요약
- 최종 추천 3개
- 서비스 오퍼링 평가
- 최종 비교
- 투표용 요약

HTML이 요청되면 단순히 HTML 코드를 답변에 붙이지 말고, `assets/voting-template.html`을 기본 패턴으로 사용해 실제 `.html` 파일을 생성한다. 최종 답변에는 생성한 HTML 파일의 클릭 가능한 경로를 제공한다.

## FitCloud Company Context

`data/company-context.yaml`을 기본 기준으로 사용한다.
사용자가 더 최신 맥락을 제공하면 이번 실행에서는 그것을 우선한다.
기본 기준이 부족하면 어떤 회사 정보가 있으면 평가가 개선되는지 말한다.

## Research Source Rules

세부 규칙은 `references/research-sources.md`를 사용한다.
조사 단계에서는 해당 파일의 조사 소스 우선순위, 최소 근거 기준, 소스별 주의사항을 따른다.

## HTML Output Rules

HTML 요청 시 `assets/voting-template.html`을 사용해 실제 `.html` 파일을 생성한다.

다음 표현은 모두 HTML 생성 요청으로 처리한다.

- "HTML로 보고 싶어"
- "HTML로 만들어줘"
- "투표용 HTML"
- "사이트/페이지로 보고 싶어"
- "결과를 브라우저에서 보고 싶어"

HTML 요청을 받은 경우 최종 산출물은 반드시 `.html` 파일이어야 한다. 대화 답변에는 요약만 짧게 쓰고, HTML 파일 링크를 제공한다.

HTML에는 다음을 포함한다.

- 최종 주제 3개 카드
- 점수표
- 점수 산정 이유 요약
- 회사 적합성 근거
- 근거 자료 요약
- service offering badge
- radio-based vote selection
- localStorage save/restore
- copy result action
- reset vote action
- static HTML은 단일 브라우저 투표만 저장하며 팀 집계를 제공하지 않는다는 안내

## Response Rules

- 교육 시간이 없으면 조사 전에 질문한다.
- 사용자에게 과거 주제를 묻기 전에 FitCloud 올해 workshop 이력을 먼저 확인한다.
- 가능하면 AWS What's New 확인에는 AWS Knowledge Base MCP를 먼저 사용한다.
- 외부 영상 트렌드에는 AI Engineer YouTube와 Lenny's Podcast를 우선 확인한다.
- 평가에는 회사 맥락과 company fit을 포함한다.
- 평가 기준과 점수 산정 이유를 포함한다.
- 선호/보너스/보정 컬럼을 추가하지 않는다.
- 올해 FitCloud workshop과 명확히 중복되는 주제는 추천하지 않는다.
- 확인하지 않은 소스를 확인했다고 말하지 않는다.
- 사용할 수 없었던 조사 소스는 명확히 밝힌다.

## Do Not

- 분위기나 트렌드 단어만으로 판단하지 않는다.
- 후보 5-7개 검토 없이 최종 3개만 바로 내지 않는다.
- 이유 없이 점수를 매기지 않는다.
- FitCloud 회사 맥락을 무시하지 않는다.
- FitCloud 올해 Immersion Day 내용을 무시하지 않는다.
- AWS Events main page를 세부 주제 근거로 사용하지 않는다.
- 사용자 후보라는 이유로 가산점을 주지 않는다.
