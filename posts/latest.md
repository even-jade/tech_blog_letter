<!-- 이 파일은 posts/2026-10-26.md의 사본입니다. 자동 생성됨. -->
# 2026-10-26 기술 블로그 모음

## [기존 LangGraph 워크플로우를 Amazon Bedrock AgentCore Runtime으로: 아이지에이웍스 클레어의 프로덕션 이관과 운영 경험](https://aws.amazon.com/ko/blogs/tech/igaworks-claire-agentic-agent-with-amazon-bedrock-agentcore-part-2/)
- 회사: AWS (아이지에이웍스 사례)
- 본문 요약: 단일 ECS 컨테이너에서 여러 LangGraph 워크플로우를 돌리며 생긴 동시성 지연과 장애 격리 문제를, FastAPI·LangGraph 코드를 재작성하지 않고 AgentCore Runtime의 /invocations, /ping 프로토콜 어댑터로 이관해 해결했습니다. Runtime 세션 식별자와 LangGraph thread_id를 분리하고, VPC 모드와 에이전트별 IAM 역할·보안 그룹으로 최소 권한을 구성했습니다. 그래프 재사용, 불필요한 LLM 호출 제거, 의존성 병렬 초기화, Redshift 워밍으로 동시성 16에서 Warm 세션 TTFT p95를 3.702초에서 0.174초로 줄였습니다.
- 주목할 point: 신규 세션 급증 시 pre-warmed 용량 초과로 콜드 스타트·초기화 실패가 생길 수 있고, 세션별 환경에 맞춰 DB 커넥션 풀을 줄이고 유휴 연결을 검증해야 합니다. Langfuse trace와 CloudWatch 구조화 로그를 묶은 관측 체계도 필요합니다.
- keyword: #AmazonBedrock #AgentCore #LangGraph #TTFT

## [아이지에이웍스 클레어의 Agentic AI PoC 여정: Amazon Bedrock AgentCore로 설계하고 평가하기](https://aws.amazon.com/ko/blogs/tech/igaworks-claire-agentic-agent-with-amazon-bedrock-agentcore-part-1/)
- 회사: AWS (아이지에이웍스 사례)
- 본문 요약: 고정형 LangGraph 워크플로우로는 운영 DB·DW를 결합한 복합 질의 처리에 한계가 있어, supervisor 그래프의 구조화 출력 기반 triage와 코드 라우팅으로 Haiku 기반 안내 경로와 Opus 기반 SQL ReAct 경로를 분리했습니다. MCP 도구 서버, AgentCore Gateway·Memory로 도구 연결과 세션 복원을 검증하고, JSONL 시나리오·assertions·trajectory 대조 기반 Evaluations 체계를 재설계했습니다.
- 주목할 point: 절대 수치 대신 실제 도구 호출 결과와 응답의 일치 여부를 평가 기준으로 삼았고, 출력 토큰 제한·도구 로딩 병렬화·MCP 세션 유지로 복합 질의 응답 시간을 약 60% 단축했습니다. trace 관측 → 수정 → 배포·평가·롤백으로 이어지는 개선 루프가 참고할 만합니다.
- keyword: #LLM #AmazonBedrockAgentCore #MCP #Evaluation

## [Search OS의 SEO와 GEO 최적화 솔루션: Amazon EKS와 Amazon CloudFront로 구축한 상품 콘텐츠 구조화 시스템](https://aws.amazon.com/ko/blogs/tech/search-os-seo-geo-optimization-eks-cloudfront/)
- 회사: AWS (Search OS 사례)
- 본문 요약: 이미지·동적 페이지 중심의 상품 정보를 검색엔진과 생성형 AI가 읽기 어려운 문제를, 분석 결과를 의미 구조가 드러나는 HTML로 변환해 제공하는 방식으로 풀었습니다. CloudFront Functions가 대상 요청만 Search OS 콘텐츠 경로로 연결해 고객사 애플리케이션 변경이 필요 없고, EKS에서 분석·HTML 생성·제공 워크로드를 분리하며 결과는 S3에 저장·재사용합니다.
- 주목할 point: KEDA(작업량 기반 파드 조절)와 Karpenter(노드 증감), ElastiCache for Valkey 비동기 큐, EC2 Spot으로 시즌성 부하와 비용을 흡수했습니다. GA4·Amplitude·Search Console·봇 로그·AI 답변 분석으로 유입부터 매출까지 측정합니다.
- keyword: #SEO #GEO #AmazonEKS #CloudFront

## [10년 만에 새로 쓴 기업홈페이지, 내부 힘으로 다시 만들기](https://medium.com/cj-onstyle/10%EB%85%84-%EB%A9%88%EC%B6%98-%EA%B8%B0%EC%97%85%ED%99%88%ED%8E%98%EC%9D%B4%EC%A7%80-%EB%82%B4%EB%B6%80-%ED%9E%98%EC%9C%BC%EB%A1%9C-%EB%8B%A4%EC%8B%9C-%EB%A7%8C%EB%93%A4%EA%B8%B0-eb4c3a315659?source=rss----c2837295b0fd---4)
- 회사: CJ온스타일
- 본문 요약: CJ ENM 커머스부문 기업홈페이지를 10년 만에 외주 없이 내부 역량으로 리뉴얼한 과정을 다룹니다. 정보구조 재설계, 반응형 UI 반영, SEO와 GEO 고려가 주요 내용입니다. (확인 가능한 범위는 요약 수준이며 세부 구현 내용은 확인하지 못했습니다.)
- 주목할 point: 오래된 기업 사이트 리뉴얼에서 검색(SEO)뿐 아니라 생성형 AI 검색 노출(GEO)까지 설계 단계에서 고려한 점이 눈에 띕니다.
- keyword: #UI/UX #SEO #GEO #반응형UI

## [Flava MCP Hub가 걸어온 길: AI 시대를 위한 배관 공사](https://techblog.lycorp.co.jp/ko/flava-mcp-hub-ai-infrastructure)
- 회사: 라인
- 본문 요약: 팀별로 MCP 서버가 늘며 중복 구현, 인증·권한 분산, 사용 현황 부재가 생기고, MCP 표준의 동적 클라이언트 연결 방식과 사내 IAM 기반 인증 사이에 Protocol Gap이 있었습니다. 이를 Connection·Proxy·Authorization·Monitoring의 4층 모델로 정리하고, stdio 기반 Connector가 OIDC 처리·토큰 캐시/자동 갱신·Bearer 헤더 주입을 맡도록 했습니다.
- 주목할 point: 오픈소스 Gateway로 시작했으나 JWKS ES512 파싱, CORS 미들웨어 순서, OOM, Rust 운영 부담 때문에 Go 기반 자체 Gateway로 전환했습니다. 현재 650개 이상 MCP 서버, 200개 이상 팀, 누적 1,150만 건 이상 도구 호출을 관측하며, 카탈로그 기반 1분 내 연결과 인증 포함 5분 내 배포를 지원합니다.
- keyword: #MCP #LLM #Gateway #인증

## [‘왜 이렇게 만들었을까’라는 질문으로 성장하는 웹 에디터 팀](https://medium.com/miridih/%EC%99%9C-%EC%9D%B4%EB%A0%87%EA%B2%8C-%EB%A7%8C%EB%93%A4%EC%97%88%EC%9D%84%EA%B9%8C%EB%9D%BC%EB%8A%94-%EC%A7%88%EB%AC%B8%EC%9C%BC%EB%A1%9C-%EC%84%B1%EC%9E%A5%ED%95%98%EB%8A%94-%EC%9B%B9-%EC%97%90%EB%94%94%ED%84%B0-%ED%8C%80-db3f60d6f6d4?source=rss----79ed61a9dcb1---4)
- 회사: 미리디
- 본문 요약: 웹 에디터 팀은 해결할 문제 정의 → 구조 설계 → 구현 순서로 일하며, 반복 로직의 싱글톤 관리, 인터페이스·추상화, 편집 동작을 위한 커맨드 패턴을 활용합니다. 애니메이션 기능은 기존 구조 분석과 설계 리뷰를 거쳐 재생 전반에 적용 가능한 인터페이스로 설계했고, Jotai 기반 상태 관리와 메모이제이션으로 다수 페이지 편집 성능을 챙깁니다.
- 주목할 point: 코드 리뷰에서 지적 대신 구조의 배경과 동작 원리를 묻는 질문 중심 피드백, 정기 회의·회고를 통한 설계 관점의 상호 학습이 팀 문화 사례로 참고할 만합니다.
- keyword: #React #Jotai #코드리뷰 #커맨드패턴

## [미리캔버스의 편집 로직을 책임지는 웹 에디터 팀 엔진 개발자들](https://medium.com/miridih/%EB%AF%B8%EB%A6%AC%EC%BA%94%EB%B2%84%EC%8A%A4%EC%9D%98-%ED%8E%B8%EC%A7%91-%EB%A1%9C%EC%A7%81%EC%9D%84-%EC%B1%85%EC%9E%84%EC%A7%80%EB%8A%94-%EC%9B%B9-%EC%97%90%EB%94%94%ED%84%B0-%ED%8C%80-%EC%97%94%EC%A7%84-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%93%A4-e98aec7d2397?source=rss----79ed61a9dcb1---4)
- 회사: 미리디
- 본문 요약: 미리캔버스 웹 에디터 팀 엔진 개발자의 역할을 소개합니다. 문서 로딩, 요소 추가·삭제·복사·붙여넣기, 실행 취소/다시 실행, 썸네일 반영 같은 핵심 편집 로직과, 디자인 요소·상태 계층과 사용자 상호작용 계층의 책임 분리를 설명합니다. 편집 영역·템플릿·요소 패널은 MFA(마이크로 프론트엔드)로 독립 서비스화했습니다.
- 주목할 point: 드래그·크기 조절 같은 실시간 조작의 즉각 반응, 수백 개 요소 동시 처리 최적화, 동시 편집 문제 대응을 다루며, 기능 추가 전 전체 구조와 영향 범위를 확인하는 습관을 강조합니다.
- keyword: #MFA #웹에디터 #상태관리 #성능

## [모던 백엔드 _ Spring Boot 4.0 개관(4)](https://www.nextree.io/modeon-baegendeu-_-spring-boot-4-0-gaegwan-4/)
- 회사: 넥스트리
- 본문 요약: Spring Boot 4.0의 API 버저닝(경로·쿼리 파라미터·요청 헤더·미디어 타입 4가지 방식), @HttpExchange 기반 선언형 HTTP 클라이언트, 재시도·동시성 제한 등 내장 회복 탄력성 기능을 소개합니다.
- 주목할 point: 마이그레이션 전 점검 대상으로 Undertow 지원 중단(Tomcat/Jetty 전환), javax.annotation → jakarta.annotation, ListenableFuture → CompletableFuture, DevTools LiveReload 비활성화가 있으며 RestTemplate 대신 선언형 클라이언트나 WebClient를 권장합니다.
- keyword: #SpringBoot4 #API버저닝 #HttpExchange #마이그레이션

## [우리가 굳이 엔지니어의 고민까지 기록하는 이유](https://tech.channel.io/kr/articles/d81e77cf)
- 회사: 채널톡
- 본문 요약: DEV POSTING은 기술적 결과뿐 아니라 문제 정의, 선택 기준, 시행착오까지 기록·공유하는 활동입니다. 매주 두 명의 엔지니어가 기술, 시스템 설계, AI, 제품, 협업·팀 운영 경험을 링크드인에 게시하며, 초안 공유와 동료 피드백을 거칩니다.
- 주목할 point: 완성도 높은 블로그·발표로 남기기 어려운 작은 개선과 미해결 고민의 기록 수단이 되고, 외부 엔지니어가 팀의 일하는 방식을 이해하는 창구가 됩니다. 결과물 중심 기록에 의사결정 배경을 함께 남기는 회고 방식으로 적용해볼 만합니다.
- keyword: #개발문화 #문서화 #DEVPOSTING

## [에이전트의 도구 실행 경로를 native tool calling으로 전환하다](https://www.nextree.io/eijeonteuyi-dogu-silhaeng-gyeongroreul-native-tool-callingeuro-jeonhwanhada/)
- 회사: 넥스트리
- 본문 요약: 프롬프트에 도구 목록을 넣고 텍스트 JSON을 파싱하던 에이전트 루프는 형식 오류 시 도구를 호출하지 못하고 종료되고, 관측 전문 재조립으로 프롬프트가 선형 증가했습니다. 엔진 포트를 messages + tools 기반으로 바꿔 Spring AI 2.0의 native tool calling(구조화된 tool_calls)을 쓰되, 도구 실행은 기존 ToolExecutionGateway가 그대로 맡도록 했습니다.
- 주목할 point: 정책·승인·감사 게이트웨이는 변경하지 않았고, 도메인 기반 도구 선택(40개 이상 도구 전량 전송 개선), TTL 캐시, 도구 불필요 요청 조기 종료를 적용했습니다. native 방식 실패에 대비한 fallback과 단위 테스트 7종도 추가했습니다.
- keyword: #SpringAI #ToolCalling #MCP #LLM

## [React 비제어 입력으로 타이핑 지연 해결하기](https://www.nextree.io/react-bijeeo-ibryeogeuro-taiping-jiyeon-haegyeolhagi/)
- 회사: 넥스트리
- 본문 요약: VoC 상세 페이지 댓글 입력 시 커서 멈춤, 한글 조합 깨짐이 간헐적으로 발생했습니다. 최상위 commentText state 갱신이 화면 전체 리렌더를 일으키고, 렌더마다 호출되는 label()이 localStorage 읽기·JSON.parse·라벨 맵 복사를 반복하는 것이 원인이었습니다. 입력 영역 분리 후에도 남은 비용을 없애기 위해 ref 기반 비제어 입력으로 전환했습니다.
- 주목할 point: 제출 시점에만 inputRef.current.value를 읽고 성공 후 직접 초기화합니다. 전환 후에도 빈 입력 비활성화, 실패 시 입력 보존, 중복 등록 방지를 별도로 유지해야 하며, MUI TextField와 react-hook-form 연동 시 inputRef와 register ref 분리, React 18 StrictMode의 updater 중복 실행도 주의점입니다.
- keyword: #React #비제어컴포넌트 #성능 #react-hook-form

## [해커톤에서 탄생한 AI 회의 비서 ‘아임타임’](https://tech.imweb.me/posts/slack-meeting-scheduler-bot/)
- 회사: 아임웹
- 본문 요약: Slack 요청을 Amazon Bedrock의 Claude가 참석자·날짜·시간·회의실 조건으로 해석하고, Google Calendar API 조회와 결합해 공통 빈 시간과 회의실을 함께 제안하는 봇입니다. 후보 카드를 사용자가 확정하면 예약 코드가 재검증 후 일정을 생성하며, 사용 사례를 분석해 팀명·스레드 맥락 해석, 예약자 전용 취소·변경, 웹 기반 회의실 현황 선택 기능을 추가했습니다.
- 주목할 point: 모델에 캘린더 변경 권한을 직접 주지 않고 사용자 확정 뒤 코드가 생성·수정·삭제를 처리하며, 일정 제목·내용 대신 바쁨 여부만 조회해 개인정보 범위를 제한했습니다. 일정 변경 시 삭제·재생성 대신 시간 수정으로 참석자 응답을 유지합니다.
- keyword: #Slack #Claude #AmazonBedrock #GoogleCalendar

## [[행사안내] 네이버클라우드, IAMSEC 2026 국제 육군 M&S 전시회 참가](https://blog.naver.com/n_cloudplatform/224454007848)
- 회사: 네이버 클라우드 플랫폼
- 본문 요약: 대전에서 열리는 IAMSEC 2026 국제 육군 모델링·시뮬레이션 학술 컨퍼런스 및 전시회에 네이버클라우드가 참가한다는 행사 안내입니다. 국방 AI 모델, 국방 AI 플랫폼, 국방 특화 클라우드로 구성된 AI 풀스택 기술을 선보일 예정입니다.
- 주목할 point: 기술 심층 글이라기보다 행사 안내이며, 첨단기술 기반 전력증강과 과학화훈련체계의 미래를 논의하는 자리라는 점이 핵심입니다.
- keyword: #컨퍼런스 #국방AI #cloud
