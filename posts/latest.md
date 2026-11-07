<!-- 이 파일은 posts/2026-11-06.md의 사본입니다. 자동 생성됨. -->
# 2026-11-06 기술 블로그 모음

## [Gemini Omni 1.2 Flash 출시 등 11월 첫째 주 Google for Developers 위클리 업데이트를 지금 확인하세요!](http://developers-kr.googleblog.com/2026/11/weeklyupdate-week1.html)
- 회사: Google for Developers Korea
- 본문 요약: 11월 첫째 주에 발표된 Google 개발자 블로그 글을 제품별로 모은 주간 소식입니다. AI에서는 Gemini Omni 1.2 Flash 출시(긴 영상을 빠르고 저렴하게 처리), Android에서는 인앱 에이전트·Android 인텔리전스·Jetpack Compose 업데이트, Firebase에서는 FCM AndroidConfigV2 소식이 실렸습니다.
- 주목할 point: 본문은 각 원문 링크 목록 성격이라 세부 내용은 원문(영문 링크)을 따로 확인해야 합니다.
- keyword: #Gemini #Android #JetpackCompose #Firebase

## [인코어드의 AWS HPC 환경에서 WRF 실행하기 [2부: MPI/OpenMP 하이브리드 병렬화 튜닝 심층 분석]](https://aws.amazon.com/ko/blogs/tech/encored-wrf-2/)
- 회사: AWS (인코어드 사례)
- 본문 요약: 재생에너지 발전량 예측용 WRF 기상 시뮬레이션을 AWS HPC 인스턴스에서 운영한 경험 2부작 중 2부입니다. hpc8a 기준 MPI 프로세스와 OpenMP 스레드 비율에 따른 실행 시간과 EFA 패킷을 분석했고, 3노드 24:8 구성이 97.25분으로 가장 빨랐으며 2노드 96:2는 CPU 사용률은 가장 높았지만 더 느렸습니다.
- 주목할 point: CPU 사용률이 높다고 효율이 좋은 것은 아니므로 tightly-coupled MPI 워크로드는 EFA tx_pkts 같은 통신 지표를 함께 봐야 합니다.
- keyword: #WRF #HPC #MPI #OpenMP #EFA

## [Claude Code Skill을 활용한 레거시 백오피스 툴 개선기: 엑셀 한 행 붙여넣기로 16개 언어 완성](https://on.com2us.com/tech/claude-code-skill-backoffice-tool/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: CKEditor 기반 레거시 이벤트 운영 툴을 Claude Code와 플러그인(superpowers, frontend-design)으로 하루 만에 새로 만든 과정입니다. 엑셀에서 복사한 한 행을 붙여넣으면 16개 언어 입력 칸이 채워지며, AI가 맡은 부분과 사람이 개입해야 했던 UX·도메인 판단 지점을 함께 정리했습니다.
- 주목할 point: 기계적으로 판단 가능한 체크는 정적 분석에 맡기고 맥락 판단이 필요한 곳에만 AI를 쓰는 역할 분담 기준을 제시합니다.
- keyword: #ClaudeCode #AgentSkills #레거시리팩토링 #다국어

## [BigQuery에서 애널리틱스 원본 데이터 조회하기](https://on.com2us.com/tech/event-bigquery-raw-data-query/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: Hive 애널리틱스 이벤트 원본 데이터를 BigQuery(habq-storage)에서 SQL로 직접 조회하는 절차입니다. 환경별 조회 권한을 신청한 뒤 본인 프로젝트에서 쿼리하며, 예시 SQL은 dateTime을 UTC에서 KST로 변환하고 checksum으로 중복을 제거하며 날짜 조건으로 파티션을 제한합니다.
- 주목할 point: 원본 이벤트를 직접 확인하면 수집 누락·중복 전송·정산 집계 차이의 원인을 추적할 수 있습니다.
- keyword: #BigQuery #Hive애널리틱스 #원본데이터 #중복제거

## [마켓 정산 전에 구글·애플 예상 수익금 확인하기](https://on.com2us.com/tech/market-estimated-proceeds/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: 결제액에는 판매세가 포함될 수 있고 수수료·국가별 세금이 반영되기 전이라 실제 수익을 알기 어렵다는 문제에서 출발합니다. Hive 애널리틱스의 '예상 수익금' 메트릭이 구글 플레이·애플 앱스토어별 계산 기준으로 일 단위 추정 수익을 보여주며, 환불은 차감하지 않는 추정값입니다.
- 주목할 point: 구글은 판매세를 제외한 뒤 수수료를 적용하고 애플은 가격표의 Proceeds 비율을 쓰는 등 마켓별 계산 방식이 다릅니다.
- keyword: #예상수익금 #마켓수수료 #판매세 #정산

## [[torch.compile() 알아보기 - Part 03] PyTorch Conference 2026 참관기](https://hyper-accel.github.io/posts/torch-compile-anatomy-3/)
- 회사: 하이퍼엑셀
- 본문 요약: 2026년 10월 PyTorch Conference 참관기로 Agent, Acceleration, Ecosystem 세 키워드로 정리했습니다. 에이전트로 늘어난 PR 검증 방식, C++로 재구현한 FakeTensor, Huawei·IBM Spyre의 NPU 통합 사례(Spyre 컴파일러 스택 약 27만 줄이 Inductor 재사용으로 약 3만 8천 줄로 감소)를 소개합니다.
- 주목할 point: FakeTensor 22.3배 가속은 연산 단위 측정이며 torchbench 전체 컴파일 지표 개선은 3.7~11.6% 수준이라고 구분해 적었습니다.
- keyword: #PyTorch #torch.compile #FakeTensor #NPU

## [2026년과 이후 JavaScript의 동향 - 라이브러리와 프레임워크](https://d2.naver.com/helloworld/0627744)
- 회사: 네이버 D2
- 본문 요약: (원문 사이트 접근이 차단되어 velopers.kr 요약 기준으로 작성) 2020년 이후 React 중심으로 재편된 프런트엔드 프레임워크 생태계를 React·Angular·Vue·Svelte·Preact의 사용률과 유지 의향으로 비교하고, Signals·서버 렌더링·메타 프레임워크·Rust 기반 빌드 도구·웹 표준·AI 도구를 공통 변화 축으로 제시합니다. React 18 동시성 렌더링과 React 19 Actions·use·서버 컴포넌트 변화도 다룹니다.
- 주목할 point: npm 다운로드 수에는 CI 반복 설치가 포함되는 한계가 있고, 서버 컴포넌트 관련 역직렬화 취약점 패치가 필요하며, 프레임워크 기능보다 JS·브라우저 표준 이해가 중요하다고 짚습니다.
- keyword: #JavaScript #React #서버컴포넌트 #Signals

## [녹화 버튼 뒤에서 일어나는 일: LINE 프리미엄콜 개발기](https://techblog.lycorp.co.jp/ko/line-premium-call-recording)
- 회사: 라인
- 본문 요약: LINE 1:1 통화를 녹음·녹화하는 프리미엄콜의 Android 개발기입니다. 음성 통화가 영상 통화로 바뀌어도 같은 파일·녹화 세션에 이어 붙이고, 영상 입력 해상도가 바뀌어도 최종 프레임 크기를 유지합니다. STT는 서버가 아닌 온디바이스 모델로 처리하며 현재 일본어만 지원합니다.
- 주목할 point: 재생용 고음질 스트림과 녹음·STT용 최적화 스트림을 분리하고, 녹음엔 침묵을 남기되 STT엔 말소리 구간만 넘기는 등 목적별로 처리합니다.
- keyword: #VoIP #온디바이스STT #Android #녹화

## [누구나 디자인할 수 있는 세상을 위해 — 미리디 CEO, 창석님](https://medium.com/miridih/%EB%88%84%EA%B5%AC%EB%82%98-%EB%94%94%EC%9E%90%EC%9D%B8%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EC%84%B8%EC%83%81%EC%9D%84-%EC%9C%84%ED%95%B4-%EB%AF%B8%EB%A6%AC%EB%94%94-ceo-%EC%B0%BD%EC%84%9D%EB%8B%98-5985463584d7?source=rss----79ed61a9dcb1---4)
- 회사: 미리디
- 본문 요약: 원문 접근이 차단되어 본문을 확인하지 못했습니다. 제목상 미리디 CEO를 소개하는 인터뷰/조직 소개 성격의 글로 보입니다.
- 주목할 point: 확인 불가 (제목·회사·링크만 기록)
- keyword: #미리디 #디자인 #인터뷰

## [뱅크샐러드 '저금리 대출 대리조회' 금융위 혁신금융서비스 지정](https://corp.banksalad.com/blog/news/bs1501/)
- 회사: 뱅크샐러드
- 본문 요약: '저금리 대출 대리조회' 서비스가 금융위원회 혁신금융서비스로 지정됐다는 보도자료입니다. 고객을 대신해 대출 가심사를 신청하고 결과를 안내하며, 한 번 위임하면 반복 조회가 필요 없고 언제든 철회할 수 있습니다. 마이데이터 기반 대출 AI 에이전트의 주요 기능으로 활용될 예정입니다.
- 주목할 point: 회사는 중·저신용자의 '금리 단층' 완화에 도움이 될 것으로 전망했습니다.
- keyword: #혁신금융서비스 #마이데이터 #대출AI에이전트

## [뱅크샐러드, AI 에이전트 판단·실행 제어 기술 특허 출원](https://corp.banksalad.com/blog/news/bs1502/)
- 회사: 뱅크샐러드
- 본문 요약: AI 에이전트의 판단과 실행을 제어하는 기술로 특허 3건을 출원했습니다. 환각 오류를 막기 위해 실행 대상 판단, 수치 검증, 실행 제어 세 축을 설계했으며, DSR·LTV 등 금융 규정 계산식으로 수치를 교차 검증하고 고객에게 불리한 거래는 실행을 보류합니다.
- 주목할 point: LLM의 판단을 그대로 실행하지 않고 실행 직전 규정 기반 검증·제어 단계를 거치는 구조입니다.
- keyword: #AI에이전트 #환각 #실행제어 #금융규정

## [뱅크샐러드 데이터 기반 카드 추천⋯평균 105만원 혜택 받는다](https://corp.banksalad.com/blog/news/bs1503/)
- 회사: 뱅크샐러드
- 본문 요약: 마이데이터 기반 맞춤 카드 추천 이용 고객을 분석한 결과 평균 105만 원의 혜택을 받았다는 발표입니다. 최근 1년 소비 내역으로 카드 한 장을 추천하고 같은 소비 패턴 유지 시 늘어나는 혜택을 원 단위로 보여줍니다.
- 주목할 point: 공개된 혜택 구간 비중 합이 100%에 못 미치고 일부 구간이 빠져 있어 분포 해석엔 원자료 확인이 필요합니다.
- keyword: #마이데이터 #카드추천 #소비패턴

## [AI 에이전트를 위한 멀티모달 의사결정 모델 ‘Kanana-2-v-decide’ 오픈소스 공개](https://tech.kakao.com/posts/846)
- 회사: 카카오
- 본문 요약: 고객 문의 분류, 상품 사진 확인, 도구 선택처럼 에이전트 요청 처리 중 반복되는 의사결정에 초점을 맞춘 멀티모달 모델을 오픈소스로 공개했습니다. (원문 본문은 추출하지 못해 요약 정보 기준)
- 주목할 point: 긴 답변 생성보다 빠른 판단 결과가 필요한 에이전트 단계에 활용할 수 있습니다.
- keyword: #Kanana #멀티모달 #의사결정모델 #오픈소스

## [php2shell 취약점의 동작 원리와 원격 코드 실행(RCE) 방어 전략: PHP부터 React·Next.js(React2Shell)까지의 대응 방안](https://blog.cslee.co.kr/php2shell-vulnerability-and-rce-defense-strategy/)
- 회사: CSLEE
- 본문 요약: PHP 멀티파트 폼 처리 중 OOM과 Use-After-Free로 RCE에 이르는 PHP2Shell 공격 흐름과, Next-Action 헤더·직렬화 데이터를 노리는 React2Shell 공격 표면을 설명합니다. 패치, Next-Action 차단, Nginx·WAF 필터링과 Rate Limit 등 대응책을 제시합니다.
- 주목할 point: Next.js 내부에 React가 포함돼 의존성 스캐너가 취약 버전을 놓칠 수 있고, PHP 미사용 서비스에도 무차별 스캐닝이 유입될 수 있습니다.
- keyword: #PHP2Shell #React2Shell #RCE #WAF

## [우아한형제들의 AI 거버넌스, 플랫폼에 담다](https://techblog.woowahan.com/27890/)
- 회사: 우아한형제들
- 본문 요약: AI Studio와 AI Gateway로 LLM·Agent 사용 신청, 정책 승인, 호출 기록을 프로젝트 단위로 연결했습니다. LiteLLM 기반 공통 호출 경로, Virtual Key 기반 모델·예산·RPM/TPM 제어, Langfuse·Grafana·Slack 기반 관측을 구성했습니다.
- 주목할 point: 프롬프트 캐싱 최적화로 캐시 비율이 5%에서 97%로 오르고 요청당 비용 84% 절감, 평균 응답 시간은 0.79초에서 1.33초로 증가했습니다.
- keyword: #AI거버넌스 #AIGateway #LiteLLM #프롬프트캐싱

## [쿠버네티스 Cilium부터 AIOps까지 | Cloud Club 9기 클라우드 스터디 후기](https://library.gabia.com/contents/infrahosting/15975/)
- 회사: 가비아
- 본문 요약: Cloud Club 9기의 Cilium(CNI·eBPF·Hubble), 모의 장애 대응(SLI/SLO, Metric·Log·Trace), AIOps 배포(AI 요약·Discord 알림) 스터디 내용을 소개합니다.
- 주목할 point: iptables 대비 Cilium의 latency·throughput·CPU 사용량을 측정하고 BPF trace로 패킷 경로를 확인하는 학습 방식입니다.
- keyword: #Kubernetes #Cilium #eBPF #AIOps
