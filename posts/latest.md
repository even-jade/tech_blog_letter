<!-- 이 파일은 posts/2026-11-03.md의 사본입니다. 자동 생성됨. -->
# 2026-11-03 기술 블로그 모음

## [국내 최초 광고 MCP를 출시하며, 개발자의 역할은 어디까지 넓어졌을까?](https://medium.com/daangn/%EA%B5%AD%EB%82%B4-%EC%B5%9C%EC%B4%88-%EA%B4%91%EA%B3%A0-mcp%EB%A5%BC-%EC%B6%9C%EC%8B%9C%ED%95%98%EB%A9%B0-%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%9D%98-%EC%97%AD%ED%95%A0%EC%9D%80-%EC%96%B4%EB%94%94%EA%B9%8C%EC%A7%80-%EB%84%93%EC%96%B4%EC%A1%8C%EC%9D%84%EA%B9%8C-8dea7fe41c07)
- 회사: 당근마켓
- 본문 요약: 광고주의 질문을 중심으로 광고 조회 MCP를 설계하고 OAuth 2.1 인증과 운영 대시보드를 구축했습니다. 출시 후 사용 행태와 도그푸딩을 검증하며 AI 기반 광고 수정 기능의 다음 단계를 도출했습니다.
- 주목할 point: 도구 스펙이 아니라 사용자(광고주)의 질문에서 출발해 MCP를 설계하고, 출시 후 사용 데이터로 확장 방향을 잡은 점
- keyword: #MCP #OAuth2.1 #광고 #AI에이전트 #도그푸딩

## [Amazon Bedrock Guardrails로 Claude Enterprise에 조직의 DLP 정책 적용하기](https://aws.amazon.com/ko/blogs/tech/claude-enterprise-inference-hooks-dlp-with-bedrock-guardrails/)
- 회사: AWS
- 본문 요약: Claude Enterprise의 Inference hooks에 AWS 판정 서버를 연결해 DLP 정책을 적용하는 방식을 소개합니다. 자체 규칙과 Bedrock Guardrails를 결합해 민감정보를 검사하고, 장애 대응과 감사 로그까지 설계했습니다.
- 주목할 point: 외부 판정 서버 장애 시 동작과 감사까지 고려한 엔터프라이즈 AI 보안 설계
- keyword: #AWS #BedrockGuardrails #DLP #ClaudeEnterprise #보안

## [딸깍으로 안되는 Multi-interest 개발기](https://d2.naver.com/helloworld/9639872)
- 회사: 네이버 D2 (KREAM)
- 본문 요약: Multi-interest 추천 모델을 KREAM에 적용하며 발생한 상품 과노출 문제를 분석했습니다. 점수 성분 분리와 다양화 전략으로 노출 상품 종류를 늘리면서 구매 지표를 유지했습니다.
- 주목할 point: 모델 도입만으로 끝나지 않고 과노출 원인을 점수 성분 단위로 분해해 해결한 점
- keyword: #추천시스템 #Multi-interest #KREAM #다양성

## [[Ceph 뜯어먹기 - Part 01] CRUSH](https://hyper-accel.github.io/posts/ceph-crush/)
- 회사: 하이퍼엑셀
- 본문 요약: CRUSH는 중앙 매핑 테이블 없이 해시 기반 계산으로 객체의 저장 위치를 구하는 Ceph의 데이터 분산 알고리즘입니다. 클러스터 맵(장애 도메인 계층)과 Placement Rule, Uniform·List·Tree·Straw 등 Bucket 알고리즘별 이동량/계산 비용 트레이드오프를 설명합니다.
- 주목할 point: 모든 노드가 독립적으로 위치를 계산할 수 있어 메타데이터 병목이 없다는 점
- keyword: #Ceph #CRUSH #분산스토리지 #ObjectStorage

## [예측을 넘어 결정과 발견으로: DeciML과 NeXA를 만든 이유](https://techblog.musinsa.com/%EC%98%88%EC%B8%A1%EC%9D%84-%EB%84%98%EC%96%B4-%EA%B2%B0%EC%A0%95%EA%B3%BC-%EB%B0%9C%EA%B2%AC%EC%9C%BC%EB%A1%9C-deciml%EA%B3%BC-nexa%EB%A5%BC-%EB%A7%8C%EB%93%A0-%EC%9D%B4%EC%9C%A0-9313debb2a4f)
- 회사: 무신사
- 본문 요약: 예측 점수만으로 해결하기 어려운 개인화 문제를 '결정'과 '발견'의 관점에서 재정의했습니다. DeciML과 NeXA로 자원 배분과 탐색 경험을 표준화하고 ML 적용 범위를 넓힙니다.
- 주목할 point: 예측 정확도 중심에서 의사결정·탐색 중심으로 ML 문제를 다시 정의한 접근
- keyword: #무신사 #개인화 #DeciML #NeXA #ML플랫폼

## [AWS에서 AI 에이전트 실행 환경 격리하기 4부: Amazon Bedrock AgentCore Runtime, 관리형 샌드박스의 동작과 선택 기준](https://aws.amazon.com/ko/blogs/tech/aws-ai-agent-sandbox-eks-isolation-part-4/)
- 회사: AWS
- 본문 요약: AgentCore Runtime의 microVM 격리와 세션 관리 동작을 EKS 환경과 비교합니다. 시작 지연, 자격 증명, 유휴 회수, 과금, 확장 기준과 도입 시 주의점을 측정으로 정리했습니다.
- 주목할 point: 관리형 샌드박스와 직접 운영 방식의 선택 기준을 실측 데이터로 제시한 점
- keyword: #AWS #AgentCore #microVM #샌드박스 #EKS

## [일본 게임사와 나눈 글로벌 서비스 전략, 컴투스플랫폼 도쿄 세미나 현장](https://on.com2us.com/tech/com2us-platform-hive-tokyo-seminar-2026/)
- 회사: 게임빌컴투스플랫폼
- 본문 요약: 컴투스플랫폼이 일본 마이넷, 한국 플레이오와 도쿄에서 '한일 게임업계 세션 교류회'를 열었습니다. 한국 모바일게임 시장 리포트와 글로벌 서비스 준비 세션에서 하이브(Hive)의 로그인·결제·웹상점·데이터 분석·고객지원 기능을 소개했고, 고객사 59명이 참석했습니다.
- 주목할 point: 일본 게임사의 한국·글로벌 진출과 한국 게임사의 일본 진출을 돕는 협력 확대 계획
- keyword: #Hive #글로벌서비스 #게임 #웹상점 #세미나

## [“Epoch을 2배로 늘려줘” — 메신저와 LLM Agent로 MLOps Workflow 이어가기](https://techblog.samsung.com/blog/article/102)
- 회사: 삼성전자
- 본문 요약: 반복적인 모델 학습·파라미터 수정 과정에서 생기는 대기 문제를 다룹니다. 메신저와 LLM Agent를 연결해 자연어 요청으로 MLOps 워크플로우를 이어가는 방식을 소개합니다.
- 주목할 point: 자리를 비운 상태에서도 메신저로 학습 파라미터를 조정할 수 있는 ChatOps형 MLOps
- keyword: #MLOps #LLMAgent #메신저 #자동화

## [옮기는 것보다 증명이 어렵다](https://tech.kakao.com/posts/845)
- 회사: 카카오
- 본문 요약: 클레임 검색 색인을 변경 알림 방식에서 데이터베이스 변경 로그 기반 CDC로 전환했습니다. 누락·값·지연 세 관점에서 새 색인의 정확성을 검증하는 과정을 다룹니다.
- 주목할 point: 마이그레이션 자체보다 '새 색인이 정확하다'는 것을 증명하는 검증 설계에 초점을 둔 점
- keyword: #CDC #검색색인 #데이터정합성 #마이그레이션

## [기획서 하나로 결함 등록까지, QA AI Hub를 만들며 배운 것](https://helloworld.kurly.com/blog/ai-qa-from-spec-to-defect/)
- 회사: 마켓컬리
- 본문 요약: QA AI Hub로 기획서 분석부터 자연어 TC 실행, Jira 결함 등록까지 연결했습니다. 정답 TC·도메인 정책·이중 게이트로 생성 품질과 운영 신뢰도를 높였습니다.
- 주목할 point: LLM 생성 결과를 정답 TC와 이중 게이트로 검증해 QA 자동화의 신뢰도를 확보한 점
- keyword: #QA #AI #TC자동화 #Jira

## [아이폰 카메라로 B마트 상품을 찾는다고?](https://techblog.woowahan.com/27810/)
- 회사: 우아한형제들
- 본문 요약: 배민 앱에 Apple Visual Intelligence 기반 B마트 이미지 검색을 App Intents로 연동했습니다. 응답 지연과 시스템 제약에 대비해 이미지 압축·타임아웃·폴백 전략을 적용했습니다.
- 주목할 point: OS 레벨 시각 지능 기능에 앱 검색을 붙이면서 지연과 제약을 방어적으로 설계한 점
- keyword: #iOS #AppIntents #VisualIntelligence #이미지검색 #배민

## [[데이터센터 입문 시리즈] 같은 GPU인데 왜 성능이 다를까? 보관 장소가 만드는 차이](https://library.gabia.com/contents/infrahosting/15962/)
- 회사: 가비아
- 본문 요약: GPU 실성능은 사양뿐 아니라 냉각·전력·네트워크·랙 배치·가동률에 따라 달라집니다. 데이터센터를 비교할 때 설비 균형과 장애 복구 체계를 함께 확인해야 합니다.
- 주목할 point: GPU 스펙 비교만으로는 알 수 없는 데이터센터 인프라 요소를 체크리스트 관점으로 짚은 점
- keyword: #GPU #데이터센터 #냉각 #인프라

## [Argo Workflows와 SageMaker로 추천 ML 파이프라인 구축기](https://helloworld.kurly.com/blog/recommend-ml-pipeline/)
- 회사: 마켓컬리
- 본문 요약: Argo Workflows와 SageMaker를 결합해 추천 모델 산출물을 세대 단위로 안전하게 교체했습니다. 활성 키 기반 컷오버와 승급 게이트, 웜업으로 일일 ML 배포를 자동화했습니다.
- 주목할 point: 활성 키 컷오버와 승급 게이트로 무중단에 가깝게 모델 세대를 교체하는 구조
- keyword: #Argo #SageMaker #MLOps #추천 #배포자동화
