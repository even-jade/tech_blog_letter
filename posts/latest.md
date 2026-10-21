<!-- 이 파일은 posts/2026-10-21.md의 사본입니다. 자동 생성됨. -->
# 2026-10-21 기술 블로그 모음

## [모델만 바꿨는데 LLM 비용이 3배가 된 이유](https://medium.com/daangn/%EB%AA%A8%EB%8D%B8%EB%A7%8C-%EB%B0%94%EA%BF%A8%EB%8A%94%EB%8D%B0-llm-%EB%B9%84%EC%9A%A9%EC%9D%B4-3%EB%B0%B0%EA%B0%80-%EB%90%9C-%EC%9D%B4%EC%9C%A0-5ae60ab5108b)
- 회사: 당근마켓
- 본문 요약: Gemini에서 OpenAI GPT-5.6으로 모델을 교체한 뒤 응답 오류 없이 요청당 비용이 3.2배 늘었고, 프롬프트 캐시 히트율이 85.8%에서 2.3%로 떨어진 원인을 분석했다. GPT-5.6부터 자동 캐시 구분점이 최근 메시지 끝에만 생성되는데, 고정 지시문과 가변 본문을 한 메시지로 보내 '지시문+글 전체'만 캐시에 쓰이고 캐시 쓰기 할증 1.25배까지 붙은 것이 원인이었다.
- 주목할 point: 고정부 끝에 명시적 캐시 구분점을 두고 캐시 히트율과 비용을 운영 지표로 관리하는 해법. 모델 교체 시 오류가 없어도 캐시 정책 변화로 비용이 급증할 수 있다는 점이 핵심.
- keyword: #LLM #프롬프트캐시 #비용최적화 #모델교체

## [앱 리뷰 자동화 일주일만에 만들기](https://medium.com/wantedjobs/%EC%95%B1-%EB%A6%AC%EB%B7%B0-%EC%9E%90%EB%8F%99%ED%99%94-%EC%9D%BC%EC%A3%BC%EC%9D%BC%EB%A7%8C%EC%97%90-%EB%A7%8C%EB%93%A4%EA%B8%B0-00a798a73975)
- 회사: 원티드
- 본문 요약: 조직 개편 과정에서 담당 주체가 사라져 약 3년간 방치된 원티드 Android·iOS 앱 리뷰에 다시 답글을 달기 시작하기 위해, 일주일 만에 리뷰 답글 자동화를 구축한 경험을 공유한다.
- 주목할 point: 방치된 운영 업무를 짧은 기간 안에 자동화로 되살린 사례로, 작게 시작해 리뷰 응답을 재개한 접근이 참고할 만하다.
- keyword: #앱리뷰 #자동화 #모바일 #운영

## [2026년과 이후 JavaScript의 동향 - 브라우저 밖의 JavaScript](https://d2.naver.com/helloworld/1443473)
- 회사: 네이버
- 본문 요약: 2019년 이후 브라우저 밖 JavaScript 생태계의 변화를 Node.js 중심으로 정리한 글. 런타임의 기능 내장화와 Node.js 호환 경쟁, Node.js·Deno·Bun의 공존, Deno의 npm·Node.js 호환 전환과 Cloudflare 합류, 공급망 보안과 릴리스 정책 변화를 다룬다.
- 주목할 point: 런타임 간 경쟁이 '호환성' 중심으로 수렴하고 있고, 공급망 보안과 릴리스 정책이 런타임 선택의 중요한 기준이 되고 있다는 점.
- keyword: #JavaScript #Node.js #Deno #Bun #공급망보안

## [LLM 추론 칩 검증 이야기 1편: 칩의 정답은 어디서 오는가](https://hyper-accel.github.io/posts/chip-verification-ground-truth/)
- 회사: 하이퍼엑셀
- 본문 요약: LLM 추론 칩(LPU) 검증에서 '정답'의 출처를 다룬다. IP 레벨은 검증자가 스펙 문서만 보고 독립적으로 만든 레퍼런스 모델과 bit-exact로 비교하고, Top 레벨은 실제 AI 모델(PyTorch golden)과 기능 시뮬레이터(fsim), ZeBu 에뮬레이터 위의 RTL을 단계별로 비교한다. 허용오차는 fsim↔golden 비교 두 곳에만 두고 RTL이 걸린 비교는 모두 bit-exact로 한다.
- 주목할 point: 비교 축마다 '한 가지만 다르게' 하면 git bisect처럼 불일치 원인이 좁혀진다는 원칙. 스펙 자체가 틀리면 IP 레벨 검증은 통과하므로 스펙을 거치지 않는 golden이 필요하다는 점.
- keyword: #칩검증 #RTL #LLM추론 #AI반도체 #bit-exact

## [글로벌 최고 수준의 자체 비전 인코더, Kanana-2-vision-encoder 개발기](https://tech.kakao.com/posts/840)
- 회사: 카카오
- 본문 요약: 카카오가 from scratch로 개발한 독자 비전 인코더 Kanana-2-vision-encoder를 소개한다. Kanana-2 LLM의 가중치와 구조를 활용해 학습·추론 효율을 높였고 고해상도 이미지 처리를 지원한다.
- 주목할 point: LLM의 구조와 가중치를 비전 인코더에 재활용해 멀티모달 모델의 학습·추론 효율을 노린 점.
- keyword: #Kanana #비전인코더 #멀티모달 #LLM

## [critical-script, 배달의민족 웹뷰 로딩 성능을 30% 개선한 인라인 스크립트 로딩 전략 이야기](https://techblog.woowahan.com/27864/)
- 회사: 우아한형제들
- 본문 요약: HTML·번들 다운로드·실행·API 요청·렌더링이 직렬로 이어지던 웹뷰 로딩 워터폴을, HTML 파싱 시점의 인라인 스크립트로 초기 API 요청을 시작해 번들 로딩과 병렬화함으로써 웹뷰 LCP를 개선했다. Vite 플러그인으로 타입 공유, 페이지 인접 배치, 스크립트 크기 제한을 지원했다.
- 주목할 point: 번들 로딩과 데이터 요청을 병렬화하는 단순한 전략으로 체감 속도를 크게 개선했고, 빌드 플러그인으로 개발 경험과 안전장치(크기 제한)를 함께 챙긴 점.
- keyword: #웹뷰 #LCP #성능최적화 #Vite #프론트엔드

## [모델보다 먼저 고민한 데이터](https://www.nextree.io/modelboda-meonjeo-gominhan-deiteo/)
- 회사: 넥스트리
- 본문 요약: 행동 이력과 학습 데이터가 쌓이지 않은 초기 추천 시스템에서, 모델을 먼저 정하면 필요한 데이터가 뒤늦게 누락될 위험이 있다고 보고 모델별(속성 기반, 협업 필터링, 지도학습 랭킹) 데이터 요구사항과 행동 이벤트의 의미를 검토했다. 필수 조건은 Filtering으로 분리하고 노출·요청·응답을 연결해 기록하는 구조를 제안한다.
- 주목할 point: 추천 시점의 조건·프로필·정책까지 포함해 이벤트를 연결 기록해야 이후 모델 확장이 가능하다는 점.
- keyword: #추천시스템 #데이터설계 #이벤트로그

## [Spring Boot와 JPA로 시작하는 데이터베이스 멀티테넌시](https://www.nextree.io/spring-bootwa-jparo-sijaghaneun-deiteobeiseu-meoltiteneonsi/)
- 회사: 넥스트리
- 본문 요약: Repository마다 반복되는 테넌트 조건과 누락 시 타 테넌트 데이터 노출 위험을 줄이기 위해 Hibernate 멀티테넌시로 행·스키마·DB 분리 방식을 비교하고 테넌트별 조회 흐름을 설명한다. 요청 헤더의 테넌트 ID를 ScopedValue 기반 TenantContext에 바인딩하고, 세션 경계·네이티브 SQL·커넥션 풀 운영 시 주의점을 정리했다.
- 주목할 point: 테넌트 격리를 개별 쿼리가 아닌 프레임워크 레벨에서 보장하되, 네이티브 SQL과 커넥션 풀 같은 우회 경로를 별도로 점검해야 한다는 점.
- keyword: #멀티테넌시 #SpringBoot #JPA #Hibernate

## [[YELO Report #1] 익숙한 것을 다시 보다](https://blog.rapportlabs.kr/4050-research-customer-insight-report)
- 회사: 라포랩스
- 본문 요약: 4050 여성을 소비자가 아니라 삶·관계·나이 듦의 변화를 겪는 사람으로 연구하는 4050연구소 YELO의 첫 리포트. 화장품 선택, 노화 경험, 의류 선택의 세 생활 장면을 통해 기존 인식을 다시 살펴본다.
- 주목할 point: 소비 행동을 단일 특성으로 일반화하지 않고 생활 맥락에서 해석하려는 UX 리서치 접근.
- keyword: #UX리서치 #고객인사이트 #4050

## [Module Federation: singleton이면 당연히 하나겠죠?](https://tech.channel.io/kr/articles/c33a7784)
- 회사: 채널톡
- 본문 요약: Module Federation에서 singleton 설정만으로 해결되지 않는 React·Context 중복 로딩의 원인을 분석했다. 런타임, import 경로, pnpm 설치 사본까지 점검 기준을 제시한다.
- 주목할 point: singleton을 설정해도 import 경로나 패키지 사본 차이로 중복이 생길 수 있어, 런타임·경로·설치 구조를 함께 점검해야 한다는 점.
- keyword: #ModuleFederation #React #마이크로프론트엔드 #pnpm

## [쌓여 있는 영상과 이미지 속 그 장면, 바로 찾을 수 있다면?ㅣMedia Intelligence 프로모션 (~11/2)](https://blog.naver.com/n_cloudplatform/224449020220)
- 회사: 네이버 클라우드 플랫폼
- 본문 요약: 누적된 영상·이미지에서 원하는 장면을 찾기 어려운 미디어 관리 문제를 제시하고, 네이버클라우드 미디어 솔루션 8종을 소개하는 Media Intelligence 릴레이 프로모션(~11/2)의 첫 소식을 전한다.
- 주목할 point: 영상·스틸컷·사진이 분리 관리되어 생기는 중복 검색 문제를 AI 기반 장면 검색으로 풀겠다는 제품 소개 글.
- keyword: #MediaIntelligence #네이버클라우드 #영상검색

## [[현장 스케치] AI 데이터센터의 미래를 만나다! - Tech Week Singapore 2026](https://tech.ktcloud.com/entry/2026-10-ktcloud-tech-week-singapore-ai-datacenter-trends)
- 회사: KT 클라우드
- 본문 요약: Tech Week Singapore 2026의 AI 데이터센터 전시·컨퍼런스 현장 동향을 정리했다. 액체냉각·모듈형 구축·통합 설계 흐름과 전력·부지·투자, 지역사회 신뢰, 운영 인력 육성 과제가 논의되었다.
- 주목할 point: GPU 집적도와 발열 증가에 대응한 액체냉각과 모듈형 구축이 업계 공통 흐름이라는 점.
- keyword: #AI데이터센터 #액체냉각 #TechWeek

## [[분석] AI 데이터센터 냉방 시스템의 Fail-Safe: 마지막 방어선 래칭릴레이](https://tech.ktcloud.com/entry/2026-10-ktcloud-datacenter-cooling-fail-safe-latching-relay)
- 회사: KT 클라우드
- 본문 요약: 고집적 GPU 클러스터에서 냉방설비가 동시에 멈추면 빠르게 온도 임계치에 도달하는 위험을 다룬다. 정전뿐 아니라 PLC 오류·통신 이상·로직 리셋으로 운전 명령 신호가 사라지는 경우를 구분하고, 래칭릴레이로 최종 접점 상태를 유지하는 Fail-Safe 설계를 소개한다.
- 주목할 point: 제어 신호 소실에도 마지막 접점 상태를 유지하도록 하드웨어 레벨 안전장치를 두는 설계.
- keyword: #데이터센터 #냉방 #FailSafe #래칭릴레이

## [[인사이트] 로봇은 왜 챗봇과 GPU 수요가 다를까? 피지컬 AI 시대의 인프라 전략](https://tech.ktcloud.com/entry/2026-10-ktcloud-physical-ai-rfm-gpu-infrastructure)
- 회사: KT 클라우드
- 본문 요약: 로봇 파운데이션 모델(RFM)은 학습·시뮬레이션·엣지 추론을 함께 요구해 LLM과 다른 GPU 수요 구조를 보인다. Three Computers 구성과 Omniverse·Cosmos 기반 가상 데이터 생성, Jetson·Thor 기반 엣지 추론을 소개하며, 국내에서는 제조 데이터와 보안 요건을 고려한 피지컬 AI 인프라 전략이 중요하다고 설명한다.
- 주목할 point: 피지컬 AI는 학습, 합성데이터 시뮬레이션, 엣지 추론의 세 축으로 인프라를 설계해야 한다는 점.
- keyword: #피지컬AI #RFM #GPU #엣지추론

## [[기술해설] AI 질문 한 줄은 얼마나 많은 에너지를 쓸까? 데이터센터가 지능을 만드는 법](https://tech.ktcloud.com/entry/2026-10-ktcloud-ai-data-center-power-liquid-cooling)
- 회사: KT 클라우드
- 본문 요약: LLM의 토큰 생성이 GPU 연산, 열 발생, 데이터센터 전력 부하로 이어지는 흐름을 설명한다. 30MW급 데이터센터의 전력 인입·변압 손실·분배 구조와, GPU 랙당 최대 80kW 밀도에서 공랭의 한계, DLC와 PUE 관리의 중요성을 정리했다.
- 주목할 point: 고밀도 GPU 환경에서는 공랭이 한계에 이르러 DLC와 PUE 관리가 필수라는 점.
- keyword: #데이터센터 #전력 #DLC #PUE

## [SaaS란? 서비스형 소프트웨어의 개념·구조·과금 방식 정리](https://library.gabia.com/contents/infrahosting/15846/)
- 회사: 가비아
- 본문 요약: SaaS의 책임 범위(사업자는 애플리케이션~네트워크, 사용자는 데이터·계정·접근 권한·단말 보안), IaaS·PaaS·SaaS의 차이, 멀티테넌시 구조와 구독·사용량 기반 과금 방식을 정리했다. 도입 전 계정·데이터 관리, 이전성, SLA, 요금 구조를 확인해야 한다고 안내한다.
- 주목할 point: SaaS 도입 시 데이터 이전성과 SLA, 요금 구조를 사전에 확인해야 한다는 체크포인트.
- keyword: #SaaS #클라우드 #멀티테넌시 #과금

## [[상품소개] 온프레미스와 클라우드를 전용회선으로 잇는, 호스트센터 하이브리드 클라우드](https://blog.naver.com/n_cloudplatform/224448071155)
- 회사: 네이버 클라우드 플랫폼
- 본문 요약: 온프레미스와 네이버클라우드를 전용회선으로 연결해 두 환경을 하나의 IT 운영 환경처럼 쓰는 호스트센터 하이브리드 클라우드 출시를 소개한다. 마켓플레이스 신규 상품이며 커넥트 라인 이용료 외에 환경 간 트래픽 비용이 없는 점이 장점이다.
- 주목할 point: 전용회선 기반 연결에서 환경 간 트래픽 비용이 없다는 점.
- keyword: #하이브리드클라우드 #전용회선 #네이버클라우드

## [루프를 품은 그래프 엔지니어링: Claude Code와 OmO로 본 설계와 실행](https://insight.infograb.net/blog/2026/10/21/graph-engineering/)
- 회사: 인포그랩
- 본문 요약: 다중 에이전트 작업을 그래프로 설계하는 방법과 Claude Code·OmO의 구현 차이를 비교했다. PR 리뷰를 정확성·보안·성능 리뷰, 검증, 수정, 테스트 반복의 순환 그래프로 설계하고, Claude Code는 JavaScript 스크립트 기반 분기·반복과 pipeline()으로, OmO는 DAG(run·dependsOn)와 노드별 모델 선택, 의존성 단위 재실행으로 구현한 차이를 보인다.
- 주목할 point: 도구 구조보다 검증 기준, 모델, 셸 권한 차이가 결과 판정에 더 큰 영향을 미쳤고, 판정 없는 출력과 기각을 구분하고 비용·반복 제한·종료 조건을 사전에 정해야 한다는 점.
- keyword: #에이전트 #그래프엔지니어링 #ClaudeCode #OmO #워크플로
