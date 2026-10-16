<!-- 이 파일은 posts/2026-10-16.md의 사본입니다. 자동 생성됨. -->
# 2026-10-16 기술 블로그 모음

## [Amazon Bedrock AgentCore로 대화형 데이터 분석 에이전트를 프로덕션 아키텍처로 전환하기: SD바이오센서 사례](https://aws.amazon.com/ko/blogs/tech/amazon-bedrock-agentcore-data-analysis-agent-sdbiosensor/)
- 회사: AWS
- 본문 요약: 멀티 에이전트의 컨텍스트 왕복에 따른 지연·토큰 비용 증가와 결과 편차 문제를 해결하기 위해, 대화형 데이터 분석 에이전트를 단일 에이전트와 결정론적 도구 중심으로 재설계했습니다. AgentCore Runtime의 단일 에이전트가 버전 고정 도구 카탈로그를 호출하고 LLM은 도구 선택과 결과 설명만 맡습니다. 실행 레인 분리, 이벤트 알림, 표준 관측성으로 프로덕션 운영성을 높였습니다.
- 주목할 point: 계산·검증은 결정론적 도구에 맡기고 LLM은 해석에 집중시키면 동일 질의의 결과 편차와 비용을 함께 줄일 수 있습니다. 장시간 분석 작업은 실행 레인을 분리해 대화형 응답성을 지키는 설계가 유효합니다.
- keyword: #AWS #AgentCore #Bedrock #데이터분석에이전트 #관측성

## [Gemini 4 Argon 성능 등 10월 셋째 주 Google for Developers 위클리 업데이트를 지금 확인하세요!](http://developers-kr.googleblog.com/2026/10/weeklyupdate-week3.html)
- 회사: Google for Developers
- 본문 요약: 10월 셋째 주 AI, Android, Google Play 관련 개발자 업데이트를 모아 소개한 위클리 글입니다. Gemini 4 Argon, Google OAuth의 DPoP, 개발 환경 및 Play 기능 소식이 포함됩니다.
- 주목할 point: 한 주간의 Google 개발자 제품군 소식을 한 번에 훑어볼 수 있어 AI 모델 변화와 인증 보안(DPoP), Android·Play 정책 변화를 빠르게 따라가기에 좋습니다.
- keyword: #Gemini #Android #GooglePlay #OAuth #DPoP

## [폭풍우의 끝에서 제타民을 만나다](https://blog.scatterlab.co.kr/tokyozetamin-376706)
- 회사: 스캐터랩 핑퐁
- 본문 요약: 폭풍우 속에서 열린 하라주쿠 첫 오프라인 이벤트에 200명 이상이 방문해 일본 유저의 높은 애정을 확인한 후기입니다. 야외 탐색 이벤트가 당일 취소되자 카페 방문 안내로 빠르게 전환했고, 유저 인증·설문 보드·메시지 게시판·굿즈 제공으로 구성했습니다. 오픈 전 대기열이 생겼고 메인 굿즈는 90분 내 소진됐습니다.
- 주목할 point: 온라인 지표만으로 알 수 없던 유저와의 실제 접점을 설문과 손글씨 메시지로 확보했고, 현장 반응을 바탕으로 공간·굿즈·대기 경험을 확장한 다음 이벤트를 준비합니다. 소규모 팀이 장소 섭외부터 운영까지 직접 수행한 사례입니다.
- keyword: #스캐터랩 #제타 #오프라인이벤트 #커뮤니티 #일본

## [CJ올리브영의 AI 기반 운영 이슈 분석과 일일 점검 자동화](https://aws.amazon.com/ko/blogs/tech/cj-oliveyoung-operations-agent-bedrock/)
- 회사: AWS
- 본문 요약: 글로벌 프로모션 장애 시 로그 분석, 고객 영향 산정, 보상안 검토가 개발 담당자에게 의존하던 문제를 AI 에이전트로 해결했습니다. Amazon Bedrock과 Strands Agents SDK 기반으로 인시던트 분석과 데일리 헬스 체크 에이전트를 만들고, Datadog 관측 데이터와 OpenSearch의 주문·쿠폰·가격 데이터를 조회합니다.
- 주목할 point: 계산·판정은 코드로 고정하고 LLM은 해석만 맡겨 신뢰성을 확보했으며, 그 결과 인시던트 대응 시간을 단축했습니다. 운영 점검 자동화에서 LLM의 역할 경계를 정하는 좋은 참고 사례입니다.
- keyword: #AWS #Bedrock #StrandsAgents #인시던트대응 #운영자동화

## [회의실을 벗어나 잔디밭으로! 여기어때 전사 가을 운동회 현장](https://techblog.gccompany.co.kr/%ED%9A%8C%EC%9D%98%EC%8B%A4%EC%9D%84-%EB%B2%97%EC%96%B4%EB%82%98-%EC%9E%94%EB%94%94%EB%B0%AD%EC%9C%BC%EB%A1%9C-%EC%97%AC%EA%B8%B0%EC%96%B4%EB%95%8C-%EC%A0%84%EC%82%AC-%EA%B0%80%EC%9D%84-%EC%9A%B4%EB%8F%99%ED%9A%8C-%ED%98%84%EC%9E%A5-7d072429c14a)
- 회사: 여기어때
- 본문 요약: 여기어때가 9월 말 진행한 전사 가을 운동회 현장을 소개하는 컬처 라운지 게시글입니다. 사내 구성원의 교류를 위한 문화 행사 소식을 다룹니다.
- 주목할 point: 구성원 간 교류를 위한 오프라인 사내 행사 사례로, 조직 문화 활동을 기획할 때 참고할 수 있습니다.
- keyword: #여기어때 #조직문화 #사내행사

## [모두의주차장 AI 음성 주차 개발기: AWS AI-DLC 워크숍에서 출시까지](https://aws.amazon.com/ko/blogs/tech/modooparking-ai-voice-parking-ai-dlc/)
- 회사: AWS
- 본문 요약: 최대 12단계, 약 2분이 걸리던 주차권 구매 과정을 이동 중에도 쉽게 하기 위해, AI-DLC로 기존 텍스트 주차 에이전트에 Amazon Transcribe 기반 STT와 Amazon Polly 기반 TTS를 이틀 만에 연결해 MVP를 검증했습니다. 음성 재입력 문제는 턴제로 해결하고 음성 전용 UX를 베타 출시했습니다.
- 주목할 point: 결제 후 1시간 내 입차 비율 62%라는 데이터로 이동 중 구매 시나리오를 근거 있게 도출했으며, AI-DLC로 요구사항·사용자 스토리·작업 계획을 정리해 짧은 기간에 검증했습니다.
- keyword: #AWS #AI-DLC #음성에이전트 #STT #TTS

## [AWS Elemental MediaConvert와 Amazon Bedrock으로 VOD 자동 챕터 생성하기](https://aws.amazon.com/ko/blogs/tech/generating-vod-auto-chapters-with-mediaconvert-and-amazon-bedrock/)
- 회사: AWS
- 본문 요약: MediaConvert의 샷 전환 후보와 Transcribe 스크립트를 Bedrock에 제공해 VOD 챕터를 자동 생성합니다. MediaConvert 단일 잡으로 HLS, 샷 전환 리포트, 음성 파일, 썸네일 타일을 동시에 만들고, AI 결과는 코드로 검증합니다.
- 주목할 point: 스크립트 기반 AI 시각과 실제 화면 전환 시각이 어긋나는 문제를 샷 전환 후보로 보정해 자연스러운 탐색 경험을 구성한 점이 핵심입니다. 썸네일 타일로 대표 이미지까지 함께 제공합니다.
- keyword: #AWS #MediaConvert #Bedrock #VOD #챕터생성

## [AI로 만든 앱, 실제 서비스가 되려면? - 오늘의집 AI 개발 플랫폼 구축 오디세이](https://www.bucketplace.com/post/2026-10-16-ai%EB%A1%9C-%EB%A7%8C%EB%93%A0-%EC%95%B1-%EC%8B%A4%EC%A0%9C-%EC%84%9C%EB%B9%84%EC%8A%A4%EA%B0%80-%EB%90%98%EB%A0%A4%EB%A9%B4-%EC%98%A4%EB%8A%98%EC%9D%98%EC%A7%91-ai-%EA%B0%9C%EB%B0%9C-%ED%94%8C%EB%9E%AB%ED%8F%BC-%EA%B5%AC%EC%B6%95-%EC%98%A4%EB%94%94%EC%84%B8%EC%9D%B4/)
- 회사: 오늘의집
- 본문 요약: AI 코딩 도구로 만든 앱을 실제 서비스로 배포하기 위한 AI 개발 플랫폼 '올리고'를 구축한 과정을 소개합니다. 하네스로 보안·DB·QA·승인 절차를 통합해 비개발자도 안전하게 배포할 수 있게 했습니다. 요구사항을 PRD·사용자 시나리오로 만들고 풀스택 앱 생성, 개발·운영 환경 단계 배포로 이어집니다.
- 주목할 point: 인프라·인증·DB·보안 검토의 복잡성과 담당 조직별 검토 순서를 플랫폼이 흡수해, AI로 만든 앱이 실서비스로 넘어가는 병목을 줄이는 접근입니다.
- keyword: #오늘의집 #AI개발플랫폼 #하네스 #비개발자 #배포

## [실행은 도메인별로, 문맥은 한 레포에](https://toss.tech/article/dw-airflow-migration)
- 회사: 토스
- 본문 요약: 400여 DAG가 모인 단일 중앙 DW Airflow 클러스터의 도메인 간 배치 지연과 장애 전파 문제를 해결하기 위해, Strangler Fig 방식으로 중앙 DW를 유지한 채 도메인별 Airflow 클러스터와 dbt 선언형 파이프라인으로 단계적으로 이전했습니다. 단일 레포에 의존성과 지표 문맥을 모아 운영 복잡도와 에이전트 탐색 비용을 낮췄습니다.
- 주목할 point: 서비스 중단 없이 점진 이전하는 전략과, 테이블 생성 주체·의존 관계를 한 레포에 선언적으로 모아 사람과 AI 에이전트 모두가 파악하기 쉽게 만든 점이 인상적입니다.
- keyword: #토스 #Airflow #dbt #데이터웨어하우스 #StranglerFig

## [토스뱅크가 패키지를 관리하는 방식 #2: 토스뱅크 패키지의 세 가지 기준](https://toss.tech/article/package-management-2)
- 회사: 토스
- 본문 요약: 패키지의 문법과 모듈 구조는 유지하고 환경별 변환과 번들링은 호스트에 맡기는 방식을 설명합니다. 패키지 빌드 단계에서는 TypeScript를 JavaScript로 변환하고, 호스트 단계에서 실행 환경별 문법 변환과 최종 번들링을 수행합니다. declaration sourcemap과 원본 파일을 제공해 IDE에서 구현 추적과 디버깅을 지원합니다.
- 주목할 point: 호스트별 브라우저·런타임 지원 범위 차이에 따른 호환성 검증 부담을 줄이면서, 사용처에서 패키지 원본 코드를 확인할 수 있게 하는 것이 핵심 기준입니다.
- keyword: #토스뱅크 #패키지관리 #TypeScript #sourcemap #번들링

## [롯데백화점의 생성형 AI 기반 파트너 제안 채널 ‘AI 비즈센터’ 구축기](https://aws.amazon.com/ko/blogs/tech/lotte-department-store-ai-biz-center/)
- 회사: AWS
- 본문 요약: 생성형 AI로 파트너사의 제안서 작성부터 담당 부서 연결까지 지원하는 AI 비즈센터를 구축했습니다. 의도 분류로 일반 Q&A와 입점·제휴 제안을 분기하고, OpenSearch 하이브리드 검색과 LLM 교차 검증으로 부서 후보를 추천합니다. 다단계 검색과 사용자 확인 절차로 부서 매칭 정확도를 25.58%에서 83.72%로 개선했습니다.
- 주목할 point: 오픈 후 2개월간 제안 접수가 전년 동기 대비 160% 증가했고 제안 고객의 약 25%가 AI 작성 기능을 활용했습니다. 낮은 매칭 신뢰도에서는 사용자 선택으로 전환하는 Human-in-the-Loop와 Presigned POST 기반 직접 업로드로 WAF 오탐을 피한 점이 실무 포인트입니다.
- keyword: #AWS #Bedrock #OpenSearch #HumanInTheLoop #롯데백화점

## [AI로 E2E 회귀 테스트 자동화하기: ‘딸깍’을 파이프라인으로 바꾸기까지](https://techblog.lycorp.co.jp/ko/ai-e2e-test-automation)
- 회사: 라인
- 본문 요약: AI 생성 E2E 테스트의 위양성을 줄이기 위해 명세, 게이트, 변형 검증, 리뷰 패킷으로 이어지는 파이프라인을 구축했습니다. 수동 회귀 테스트 98개를 자동화하고 범위를 196개로 확대했습니다. 다중 컨테이너의 임의 선택과 복수 검증 항목 누락 같은 위험을 단계별로 통제합니다.
- 주목할 point: AI가 만든 Playwright 테스트가 통과해도 원래 테스트 의도와 다를 수 있다는 점이 핵심 문제이며, 검증 단계를 파이프라인으로 고정해 해결했습니다.
- keyword: #라인 #E2E테스트 #Playwright #AI테스트 #회귀테스트

## [모던 백엔드 - Spring Boot 4.0 개관(2)](https://www.nextree.io/modeon-baegendeu-spring-boot-4-0-gaegwan-2/)
- 회사: 넥스트리
- 본문 요약: Spring Boot 4.0 전환 시 Jackson 3, JSpecify, HTTP 클라이언트 변경점을 살펴봅니다. 레거시 API 제거와 런타임·빌드 리스크를 줄이는 점진적 마이그레이션을 안내합니다.
- 주목할 point: Jackson 패키지 좌표 변경과 날짜·시간 직렬화 기본 동작 변화가 런타임 결함으로 이어질 수 있어 주의가 필요합니다.
- keyword: #SpringBoot #Jackson3 #JSpecify #마이그레이션

## [모던 백엔드 - Spring Boot 4.0 개관(1)](https://www.nextree.io/modeon-baegendeu-spring-boot-4-0-gaegwan-1/)
- 회사: 넥스트리
- 본문 요약: Spring Boot 4.0 전환의 배경과 핵심 베이스라인 격상에 따른 변화를 살펴봅니다. Java 25, Spring Framework 7.0, Jakarta EE 11, Jackson 3, 차세대 테스트 엔진이 동시에 격상되며, 런타임 호환성과 자동 구성 분할을 중심으로 마이그레이션 위험을 점검합니다.
- 주목할 point: Spring Boot 3.x의 오픈소스 지원 종료에 대응해야 하는 상황에서, 컴파일 성공만으로는 확인하기 어려운 런타임 침묵 결함 위험을 점검해야 합니다.
- keyword: #SpringBoot #Java25 #SpringFramework7 #JakartaEE11

## [모던 백엔드 - 신규 문법 적용 리팩토링](https://www.nextree.io/modeon-baegendeu-singyu-munbeob-jeogyong-ripaegtoring/)
- 회사: 넥스트리
- 본문 요약: Java 25의 모듈 임포트와 유연한 생성자 본문을 게시판 프로젝트에 적용한 리팩토링 실습입니다. 이름 충돌과 프롤로그에서의 인스턴스 참조 제한도 함께 다룹니다. 원시 타입 패턴과 컴팩트 객체 헤더는 실습 대상에서 제외했습니다.
- 주목할 point: java.io, java.nio, java.util 등 다수 임포트를 모듈 임포트로 줄이는 효과와, 이름 충돌 가능성이라는 트레이드오프를 함께 확인할 수 있습니다.
- keyword: #Java25 #모듈임포트 #리팩토링 #넥스트리

## [AWS에서 Teamcenter Simulation으로 제품 개발 가속하기](https://aws.amazon.com/ko/blogs/tech/accelerating-product-engineering-with-teamcenter-simulation-on-aws/)
- 회사: AWS
- 본문 요약: AWS에서 Teamcenter Simulation을 운영해 PLM과 시뮬레이션 데이터를 연결하는 방안을 소개합니다. 여러 가용 영역의 EC2 기반 Teamcenter 서버, RDS for Oracle, FSx for NetApp ONTAP 또는 EFS를 구성하고, WorkSpaces Applications로 GPU 기반 클라이언트를 제공합니다.
- 주목할 point: 제품 변형과 시뮬레이션 증가로 늘어나는 CAE 데이터 관리 부담과 온프레미스 확장성·복구 한계를 확장성, 보안, 고가용성, GPU 스트리밍으로 해소하는 구조입니다.
- keyword: #AWS #Teamcenter #PLM #CAE #시뮬레이션

## [AWS ParallelCluster로 Teamcenter 시뮬레이션 가속하기](https://aws.amazon.com/ko/blogs/tech/accelerate-teamcenter-simulation-with-aws-parallelcluster/)
- 회사: AWS
- 본문 요약: Teamcenter Simulation과 AWS ParallelCluster를 결합한 클라우드 HPC 시뮬레이션 구조를 소개합니다. FSx for NetApp ONTAP 기반 Teamcenter 서버와 Linux 기반 ParallelCluster가 스토리지를 공유하고, Slurm 작업 제출, 컴퓨팅 노드 자동 프로비저닝, 결과 자동 수집·버전 관리 흐름을 제공합니다.
- 주목할 point: 대규모 CFD·FEA 수요 증가 속에서 작업 대기열, 대용량 파일 전송, 데이터 버전 불일치로 인한 지연을 줄이고 탄력적 확장과 비용 최적화를 동시에 노립니다.
- keyword: #AWS #ParallelCluster #Slurm #HPC #Teamcenter

## [AWS X 로앤컴퍼니 AI 해커톤 : VOC 자동 조사 에이전트 “민붕이” 개발기](https://aws.amazon.com/ko/blogs/tech/law-and-company-hackathon-voc-agent/)
- 회사: AWS
- 본문 요약: 월 평균 29건의 VoC를 건당 약 80분씩 수작업으로 조사하던 부담을 줄이기 위해 AI 에이전트 '민붕이'를 설계·운영한 사례입니다. MCP 기반 단일 서버 구조에 보안·검증·비용 통제를 적용했고, 유사 사례 조사, 코드 원인 추적, Jira 티켓·보고서·Notion 문서화를 맡깁니다.
- 주목할 point: 검증·담당자 지정·코드 수정은 사람이 맡고 조사와 초안 작성은 에이전트가 맡는 역할 분담이 핵심이며, 실무 투입을 위한 보안·비용 통제를 함께 설계했습니다.
- keyword: #AWS #MCP #VoC #AI에이전트 #로앤컴퍼니

## [한화오션 조선 현장의 다국어 소통을 돕는 AWS 기반 OTalk 활용 사례](https://aws.amazon.com/ko/blogs/tech/hanwha-ocean-flitto-otalk/)
- 회사: AWS
- 본문 요약: 한화오션이 조선소의 소음과 전문 용어 문제를 해결하기 위해 AWS 기반 AI 통번역 앱 OTalk을 도입했습니다. 고소음 환경 음성 인식, 조선 용어 반영, 1:1·1:N 통역을 지원하며, 현장 용어집과 사투리·소음 음성 데이터로 특화 모델을 학습하고 Amazon Bedrock으로 보정합니다.
- 주목할 point: 일반 번역 앱으로 대응하기 어려운 다국적 작업자 환경에서 작업 지시와 안전 정보 전달 공백을 줄였고, 격리된 인프라로 번역 품질과 활용 범위를 넓혔습니다.
- keyword: #AWS #Bedrock #OTalk #음성번역 #한화오션

## [인코어드의 AWS HPC 환경에서 WRF 실행하기 [1부: HPC 전용 인스턴스 선택과 비용 최적화]](https://aws.amazon.com/ko/blogs/tech/encored-wrf-1/)
- 회사: AWS
- 본문 요약: 1km 해상도 WRF 기상 시뮬레이션을 목표 시간 안에 완료하면서 비용을 최소화하기 위해, hpc7g·hpc6a·hpc8a 인스턴스에서 실행 시간과 온디맨드 총비용을 비교했습니다. hpc7g 10노드가 가장 경제적이었고, hpc8a는 hpc6a를 대체할 가능성을 보였습니다.
- 주목할 point: 도메인별 MPI rank 상한과 통신 부담 때문에 코어·노드를 늘려도 선형 성능 향상이 어렵습니다. 물리 코어를 MPI rank와 OpenMP thread로 분배하고 EFA 통신을 활용하는 구성을 함께 비교했다는 점이 참고가 됩니다.
- keyword: #AWS #HPC #WRF #hpc7g #비용최적화
