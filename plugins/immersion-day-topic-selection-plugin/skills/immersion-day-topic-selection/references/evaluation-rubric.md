# 평가 기준

Immersion Day 후보 주제를 점수화할 때 이 기준을 사용한다.

## 점수 공식

```text
최종 점수 =
최신성
+ 고객 문제 가설 신뢰도
+ hands-on 가능성
+ AWS 서비스 적합성
+ 차별성
+ 발표/진행 가능성
+ 서비스 오퍼링 가능성
+ 재사용성
+ 회사 적합성
```

각 기준은 1-5점으로 평가한다. 2점과 4점은 근거가 1/3/5 기준 사이에 있을 때만 사용한다.

## 점수 설명 규칙

점수는 평가자가 옆에 없어도 이해되어야 한다.

각 후보에는 다음을 포함한다.

- 기준별 숫자 점수
- 왜 이 점수인지
- 1-4점인 경우 왜 더 높은 점수가 아닌지

형식:

```text
기준:
- 점수:
- 왜 이 점수인가:
- 왜 더 높은 점수가 아닌가:
```

5점인 경우 `왜 더 높은 점수가 아닌가`에는 `5점 기준을 충족함`처럼 명확히 적는다.

`적합함`, `최신 트렌드`, `일부 리스크`처럼 모호한 표현만 쓰지 않는다. 반드시 근거, 제약, 부족한 조건을 같이 적는다.

예시:

```text
hands-on 가능성:
- 점수: 3
- 왜 이 점수인가: 4시간 안에 guided demo는 가능하지만, 참가자 실습은 사전 데이터, IAM 권한, 준비된 notebook에 의존한다.
- 왜 더 높은 점수가 아닌가: clean account에서 참가자가 전체 lab을 안정적으로 완주하기 어렵기 때문에 5점은 아니다.
```

```text
회사 적합성:
- 점수: 4
- 왜 이 점수인가: FitCloud의 AWS workshop, PoC 발굴, MSP/운영 후속 제안과 연결된다.
- 왜 더 높은 점수가 아닌가: 반복 제공을 위한 demo asset, architecture diagram, delivery playbook이 아직 필요하다.
```

## 1/3/5 점수 기준

| 기준 | 5점 | 3점 | 1점 |
|---|---|---|---|
| 최신성 | 최근 12개월 내 AWS와 외부 AI Engineering 신호가 모두 강함 | AWS 또는 외부 신호 중 하나만 있거나 12-24개월 전 신호임 | 오래된 일반 주제이며 최근 신호가 약함 |
| 고객 문제 가설 신뢰도 | 내부 직접 근거가 있거나, 외부 근거와 FitCloud 고객군 적합성, 구매자, 예산 경로, 반복 use case가 모두 강함 | 고객 문제 가설은 그럴듯하지만 구매자, 긴급도, 예산 경로가 아직 추정임 | 실제 고객 문제보다 트렌드 소개 또는 기술 관심에 가까움 |
| hands-on 가능성 | 주어진 시간 안에 명확한 결과물까지 실습 가능 | demo shortcut 또는 사전 준비가 꽤 필요함 | live hands-on으로 진행하기 위험함 |
| AWS 서비스 적합성 | AWS 서비스가 가치 제안의 중심임 | AWS가 유용하지만 차별화 요소가 명확하지 않음 | AWS 연결이 부수적으로 느껴짐 |
| 차별성 | 흔한 RAG/chatbot/intro 주제와 명확히 다름 | 익숙한 주제지만 각도가 일부 다름 | 반복되거나 흔한 주제와 매우 유사함 |
| 발표/진행 가능성 | 발표자가 설명, demo, Q&A를 안정적으로 진행 가능 | SME 또는 보강 자료가 필요함 | 너무 복잡하거나 fragile해서 진행 위험이 큼 |
| 서비스 오퍼링 가능성 | 반복 가능한 PoC/consulting/build/operations package로 전환 가능 | 일부 고객에게는 가능하지만 customization 필요 | 유료 후속 제안으로 전환하기 어려움 |
| 재사용성 | 여러 산업과 고객에 쉽게 재사용 가능 | 일부 module만 재사용 가능 | 대부분 one-off 성격임 |
| 회사 적합성 | FitCloud의 startup/SMB 중심 고객군에 적용 가능하고, enterprise-only 전제 없이 FitCloud asset/offering과 연결됨 | 일부 enterprise 전제가 있지만 startup/SMB 시나리오로 축소 가능함 | 대형 enterprise 조직, 복잡한 governance, 대규모 데이터/보안 조직 또는 FitCloud 주요 고객군과 맞지 않는 sales motion이 전제임 |

## 고객 문제 가설 신뢰도

모든 주제에 내부 고객 사례를 요구하지 않는다.

내부 직접 근거가 있으면 강한 신호다. 하지만 내부 근거가 없어도 아래 신호가 여러 개 강하면 4-5점을 줄 수 있다.

- FitCloud 주요 고객군과 명확히 맞음
- AWS 공식 자료 또는 시장 자료에서 반복적으로 등장
- 비용, 운영, 보안, 생산성, 매출, 개발 속도 등 구체적인 비즈니스/운영 문제와 연결됨
- 구매자 또는 의사결정자가 식별됨
- 예산 또는 조직적 노력이 투입될 가능성이 있음
- PoC, 진단, 구축, 운영, governance, 교육 등 다음 액션이 명확함

점수 가이드:

- 5점: 내부 직접 근거가 있거나, 외부 근거와 고객군 적합성, 구매자, 예산 경로, 반복 use case가 모두 강함
- 4점: 내부 직접 근거는 없지만 AWS/시장 근거, FitCloud 고객군 적합성, 구매자/예산 경로가 강함
- 3점: 가설은 그럴듯하지만 구매자, 긴급도, 예산 경로가 아직 추정임
- 2점: 일부 좁은 고객군에만 맞거나 기술 호기심에 가까움
- 1점: 실제 고객 문제보다 트렌드 교육에 가까움

## 회사 적합성과 고객 믹스

FitCloud의 기본 고객 믹스는 startup 60%, SMB 25%, public sector 10%, enterprise 5%이다.

enterprise-only 주제는 자동 제외하지 않는다. 다만 startup/SMB 고객에게 맞게 재구성할 수 없고 현재 FitCloud 오퍼링과도 연결이 약하면 company fit 고득점을 주지 않는다.

회사 적합성 점수 가이드:

- 5점: startup/SMB 중심 고객에게 바로 적용 가능하고, 대형 enterprise 전용 governance나 대규모 데이터 플랫폼을 전제로 하지 않으며, FitCloud workshop, PoC 발굴, MSP, migration, DevOps, cost, security, AI/ML 오퍼링과 연결됨
- 4점: 고객/오퍼링 적합성은 강하지만 반복 제공을 위한 demo, delivery playbook, reference architecture가 필요함
- 3점: 일부 enterprise 전제가 있으나 startup/SMB 시나리오로 축소 가능함
- 2점: enterprise 또는 regulated customer 중심이라 FitCloud 주요 고객군과의 적합성이 제한적임
- 1점: 대형 enterprise 조직, 복잡한 multi-account governance, 성숙한 platform/security team, 대규모 데이터 인프라가 필수 전제임

enterprise 성격이 강한 주제는 낮게 점수화하기 전에 먼저 재구성을 시도한다.

- enterprise governance → lightweight guardrails
- large data platform → PoC-scale data workflow
- organization-wide rollout → team-level adoption
- complex operations program → lean operations/MSP scenario

## 필수 산정 근거

숫자만 제공하지 않는다. 모든 후보에는 다음을 포함한다.

```text
후보:
- 총점:
- 기준별 점수:
  - 기준:
    - 점수:
    - 왜 이 점수인가:
    - 왜 더 높은 점수가 아닌가:
- 높은 점수 이유:
- 감점 또는 리스크 이유:
- 회사 적합성 근거:
- 사용한 근거:
```

근거 유형:

- AWS Knowledge Base MCP
- AWS 공식 docs/blog/What's New/events/workshops
- AI Engineer, Lenny's Podcast 등 우선 YouTube 소스 또는 외부 AI Engineering 근거
- FitCloud 이전 workshop 이력
- FitCloud 회사 맥락
- 사용자 제공 제약사항

## 서비스 오퍼링 가능성

High / Medium / Low로 평가한다.

High:

- 명확한 구매자 문제
- 반복 가능한 architecture
- PoC에서 유료 delivery로 이어지는 경로
- consulting, build, governance, operations, enablement package로 전환 가능
- 여러 고객 또는 산업에서 재사용 가능

Medium:

- 일부 고객군에는 작동함
- customization 필요
- PoC로는 유용하지만 packaging이 명확하지 않음

Low:

- 대부분 트렌드 교육에 가까움
- 구매자 문제가 약함
- package화하기 어려움
- AWS 서비스 차별성이 약함

## 최종 선정 규칙

최종 3개는 단순히 총점 상위 3개가 아닐 수 있다. 주제가 너무 겹치면 portfolio 구성을 우선한다.

선호 구성:

- stable/high-confidence topic 1개
- trend-attractive topic 1개
- offering-oriented topic 1개

총점 순서와 다른 선택을 했다면 이유를 설명한다.
