# 조사 소스

조사 단계에서 이 파일을 사용한다. 가능하면 1차/공식 소스를 우선하고, 최종 출력에는 사용한 URL을 포함한다.

## 기존 FitCloud Workshop

주요 확인 URL:

- `https://workshop.fitcloud.co.kr/immersion-day`

확인 절차:

1. 목록 페이지를 연다.
2. 올해 Immersion Day 항목을 식별한다.
3. 모든 올해 상세 페이지를 연다.
4. 작년 이전 항목은 기본 확인 대상이 아니다. 사용자가 특정 과거 주제를 제외했거나, 후보와 제목, AWS 서비스, 키워드가 명확히 겹치는 경우에만 해당 상세 페이지를 추가로 연다.
5. 다음을 추출한다.
   - 제목
   - 날짜/월
   - 교육 목표
   - 대상자
   - agenda
   - 자료 링크
   - 관련 AWS 서비스
   - 키워드
6. 확인한 workshop과 후보 주제를 비교한다.
7. 유사성을 다음 기준으로 표시한다.
   - High: 같은 AWS 서비스와 같은 시나리오 또는 고객 문제
   - Medium: 같은 AWS 서비스이지만 시나리오 또는 고객 문제가 다름
   - Low: 키워드 일부만 겹치거나 메시지와 시나리오가 다름
8. High 유사성이거나 사용자가 명시적으로 제외한 주제만 제외 또는 하향 평가한다.

기본 범위:

- 올해 Immersion Day 주제만 확인한다.
- 작년 이전 주제는 자동 제외하지 않는다.
- 올해 필터링이 불가능하면 최근 6개월 또는 최근 3-5개 Immersion Day 페이지를 확인한다.
- 올해 주제가 없으면 최근 3-5개 Immersion Day 페이지를 fallback 근거로 사용하고, fallback 근거라고 표시한다.
- AWS 서비스, 고객 문제, hands-on 시나리오, 오퍼링 경로가 크게 달라졌다면 과거 주제도 재해석할 수 있다.
- 사용자가 특정 과거 주제를 제외하라고 하면 연도와 관계없이 제외 또는 하향 평가한다.

기존 주제 유사성을 언급할 때는 근거 URL을 반드시 포함한다.
확인 범위도 반드시 적는다. 예: "올해 FitCloud Immersion Day 페이지를 확인했고, 상세 페이지 4개를 열었습니다."

## AWS Knowledge Base MCP

사용 가능하면 AWS Knowledge Base MCP를 먼저 사용한다.

AWS 근거를 web search로 찾기 전에 현재 환경에서 AWS Knowledge Base MCP를 사용할 수 있는지 확인한다.

우선 조회 대상:

- AWS What's New
- AWS 공식 문서
- AWS Blog와 서비스 발표
- 서비스 기능 제약과 hands-on 요구사항

What's New 확인:

- web search보다 MCP 결과를 우선한다.
- 서비스명, 기능명, 후보 키워드로 질의한다.
- MCP 결과를 기록하거나, MCP를 사용할 수 없었거나 결과가 부족했다고 명시한다.
- 실제 MCP 질의를 수행하지 않았다면 MCP를 사용했다고 말하지 않는다.
- MCP를 사용할 수 없으면 `"AWS Knowledge Base MCP was not available in this session."`이라고 적는다.
- AWS 공식 웹 문서로 대체 조사한 경우 AWS 근거 유형을 `"AWS official web fallback"`으로 표시한다.

## AWS 공식 웹 소스

MCP를 사용할 수 없거나 MCP 결과가 부족하면 AWS 공식 웹 소스를 사용한다.

What's New:

- `https://aws.amazon.com/about-aws/whats-new/`
- `https://aws.amazon.com/new/`

Blogs:

- `https://aws.amazon.com/blogs/aws/`
- `https://aws.amazon.com/blogs/machine-learning/`
- `https://aws.amazon.com/blogs/big-data/`
- `https://aws.amazon.com/blogs/mt/`
- `https://aws.amazon.com/blogs/security/`
- `https://aws.amazon.com/blogs/devops/`

Docs:

- Bedrock: `https://docs.aws.amazon.com/bedrock/`
- Bedrock Agents: `https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html`
- Bedrock Guardrails: `https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails.html`
- Amazon Q Developer: `https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/`
- Amazon Q Business: `https://docs.aws.amazon.com/amazonq/latest/qbusiness-ug/`
- QuickSight / Quick Suite: `https://docs.aws.amazon.com/quicksight/`
- CloudWatch: `https://docs.aws.amazon.com/cloudwatch/`
- EKS: `https://docs.aws.amazon.com/eks/`
- ECS: `https://docs.aws.amazon.com/ecs/`
- Lambda: `https://docs.aws.amazon.com/lambda/`
- Step Functions: `https://docs.aws.amazon.com/step-functions/`
- OpenSearch Service: `https://docs.aws.amazon.com/opensearch-service/`
- SageMaker AI: `https://docs.aws.amazon.com/sagemaker/`

## AWS Events와 Workshops

Events hub:

- `https://aws.amazon.com/events/`

이 페이지는 AWS의 상위 메시지와 행사/교육 포맷을 확인하는 용도로만 사용한다. 세부 기술 근거로 단독 사용하지 않는다.

세부 event/session 소스:

- re:Invent: `https://reinvent.awsevents.com/`
- AWS Summits: `https://aws.amazon.com/events/summits/`
- AWS re:Inforce: `https://aws.amazon.com/events/reinforce/`

사용 기준:

- re:Invent는 최신 AWS 서비스 발표, keynote, session catalog, builder/architecture 방향성을 확인할 때 사용한다.
- AWS Summits는 지역별 featured topics와 대중적인 교육/워크숍 메시지를 확인할 때 사용한다.
- AWS re:Inforce는 보안, identity, detection, response, governance, generative AI security 주제에 한해서 참고한다. 2026년에는 re:Inforce가 re:Invent 프로그램에 합류하므로, 독립 행사 트렌드가 아니라 2025 보안 세션/키노트 아카이브와 보안 메시지 확인용으로만 사용한다.
- AWS Innovate는 안정적인 공식 이벤트 URL로 고정하지 않는다. 필요한 경우 AWS Events hub에서 현재 열려 있는 Innovate 페이지를 검색해 확인하고, URL이 확인된 경우에만 사용한다.

Builder workshops:

- `https://builder.aws.com/build/workshops?tab=discover`

Builder workshop 검색:

- Discover tab을 사용한다.
- "이름으로 워크숍 찾기"에서 검색한다.
- 정렬은 최신순으로 시작한다.
- 필요한 경우 다음 필터를 사용한다.
  - level
  - language
  - category
  - AWS service and feature
  - duration
- 검색 키워드:
  - AI
  - generative AI
  - agent
  - Bedrock
  - Amazon Q
  - observability
  - security
  - AIOps
- 4시간 Immersion Day 기준으로 긴 workshop은 전체 채택이 아니라 module source로 본다.
- 품질과 최신성이 비슷하면 한국어 workshop을 우선한다.

## YouTube 트렌드 소스

우선 확인할 YouTube 소스:

- `https://www.youtube.com/@aiDotEngineer/videos`
- `https://www.youtube.com/@LennysPodcast`

확인 절차:

1. 각 우선 소스의 Videos tab을 확인한다.
2. 최근 영상, conference/session recording, practitioner interview, product/engineering leadership discussion을 우선한다.
3. 다음 키워드를 찾거나 훑어본다.
   - agent
   - MCP
   - RAG evaluation
   - evals
   - observability
   - guardrails
   - AI engineering
   - AIOps
   - workflow automation
   - product strategy
   - AI product adoption
   - enterprise AI adoption
   - startup AI workflows
   - PM/engineering productivity
4. 가능하면 제목, 게시일, 설명, session명, speaker, event context, 공개 transcript를 사용한다.
5. 실제로 전체 영상을 보지 않았다면 전체 영상 검토라고 말하지 않는다.
6. 영상 하나만으로 트렌드를 단정하지 않는다. 우선 YouTube 소스에서 관련 영상 2개 이상을 사용하거나, 우선 YouTube 영상 1개와 신뢰 가능한 외부 소스 1개를 함께 사용한다.
7. AI Engineer는 engineering implementation 신호로 더 강하게 본다.
8. Lenny's Podcast는 product, adoption, workflow, buyer-context 신호로 본다. AWS 기술 구현 근거로 사용하지 않는다.

최종 출력에는 다음을 포함한다.

- 영상 제목
- URL
- 채널명
- 확인한 키워드
- AWS Immersion Day 주제 선정에 왜 의미가 있는지

## 보조 외부 소스

우선 YouTube 근거가 부족할 때 사용한다.

- Latent Space
- The New Stack
- InfoQ
- 기타 신뢰 가능한 AI Engineering conference/session summary

외부 근거는 AWS delivery 가능성과 연결되어야 한다. 외부에서는 뜨겁지만 AWS hands-on 또는 FitCloud 오퍼링 가능성이 약하면 리스크로 표시한다.
