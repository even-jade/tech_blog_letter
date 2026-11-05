<!-- 이 파일은 posts/2026-11-05.md의 사본입니다. 자동 생성됨. -->
# 2026-11-05 기술 블로그 모음

## [QA 팀이 아니라 Quality Platform 팀을 만든 이유](https://flex.team/blog/2026/11/05/backend49)
- 회사: flex
- 본문 요약: AI 에이전트로 코드 변경량이 늘어나자 기존 QA 외주화 구조를 Quality Platform 방식으로 전환한 이야기입니다. 개발자가 테스트·데이터·회귀 검증 도구로 품질과 성능을 직접 확인하도록 지원합니다.
- 주목할 point: 품질 책임을 QA 전담 인력이 아니라 개발자가 셀프서비스로 지는 플랫폼 구조로 옮긴 점
- keyword: #QA #QualityPlatform #CI/CD #SpringBoot

## [딸깍으로 안되는 Multi-interest 모델 개발기](https://medium.com/kream-%EA%B8%B0%EC%88%A0-%EB%B8%94%EB%A1%9C%EA%B7%B8/%EB%94%B8%EA%B9%8D%EC%9C%BC%EB%A1%9C-%EC%95%88%EB%90%98%EB%8A%94-multi-interest-%EB%AA%A8%EB%8D%B8-%EA%B0%9C%EB%B0%9C%EA%B8%B0-27f79d039d5d?source=rss----443c5f9eb660---4)
- 회사: 크림(KREAM)
- 본문 요약: Multi-interest 추천 모델에서 특정 아이템이 과노출되는 Hubness 문제의 원인을 유저 무관 성분과 후보 집합 특성에서 분석했습니다. Centering, bias 분리, 다양성 규제로 과노출을 줄이고 평가 체계를 보완했습니다.
- 주목할 point: 모델 구조 변경만이 아니라 평가 지표까지 함께 손봐야 추천 품질 개선을 검증할 수 있다는 점
- keyword: #추천시스템 #MultiInterest #Hubness #머신러닝

## [worklog-system 주간보고 자동화 구축 경험기](https://d2.naver.com/helloworld/5037598)
- 회사: 네이버
- 본문 요약: 업무 기록을 모아 주간보고를 자동화하는 worklog-system 구축 경험입니다. 여러 기기·VPN 환경에서 중앙 서버 없이 업무 도구를 확장한 과정을 다룹니다.
- 주목할 point: 중앙 서버 없이도 분산된 환경에서 업무 기록을 모으는 가벼운 구조
- keyword: #업무자동화 #주간보고 #생산성

## [[Team Spotlight] 'IP전략팀' 갖춰진 밸류체인을 넘어 '실제로 움직이는' 밸류체인을 만듭니다.](https://www.blog-dreamus.com/post/team-spotlight-ip%EC%A0%84%EB%9E%B5%ED%8C%80-%EA%B0%96%EC%B6%B0%EC%A7%84-%EB%B0%B8%EB%A5%98%EC%B2%B4%EC%9D%B8%EC%9D%84-%EB%84%98%EC%96%B4-%EC%8B%A4%EC%A0%9C%EB%A1%9C-%EC%9B%80%EC%A7%81%EC%9D%B4%EB%8A%94-%EB%B0%B8%EB%A5%98%EC%B2%B4%EC%9D%B8%EC%9D%84-%EB%A7%8C%EB%93%AD%EB%8B%88%EB%8B%A4)
- 회사: 드림어스컴퍼니
- 본문 요약: IP전략팀이 음악 IP를 음원·플랫폼·공연·MD로 확장하는 360° 사업화를 설계하는 방식을 소개합니다. 손익·현금 흐름 관리와 이해관계자 조율로 사업 간 시너지를 만듭니다.
- 주목할 point: 기술 글이 아닌 팀 소개 성격으로, IP 사업화 관점의 조직 역할을 보여줌
- keyword: #IP전략 #팀소개 #음악

## [2026년과 이후 JavaScript의 동향 - WebAssembly](https://d2.naver.com/helloworld/7770448)
- 회사: 네이버
- 본문 요약: WebAssembly 2.0·3.0의 주요 기능과 브라우저·런타임 지원 현황을 정리했습니다. WasmGC, WASI, 문자열 상호 운용이 넓힌 활용 범위를 살펴봅니다.
- 주목할 point: WasmGC와 문자열 상호 운용으로 JS 외 언어의 웹 활용 가능성이 커지고 있다는 점
- keyword: #WebAssembly #WasmGC #WASI #JavaScript

## [GPUaaS란? 서비스형 GPU의 개념·구조·과금 방식 정리](https://library.gabia.com/contents/infrahosting/16112/)
- 회사: 가비아
- 본문 요약: GPUaaS의 IaaS 기반 책임 범위와 인스턴스·베어메탈 중심 구성 요소를 정리했습니다. 과금 방식과 GPU 메모리·클러스터 네트워크·보안 책임 등 도입 기준을 설명합니다.
- 주목할 point: 도입 전 GPU 메모리, 클러스터 네트워크, 보안 책임 범위를 체크리스트로 볼 수 있음
- keyword: #GPUaaS #클라우드 #인프라 #AI

## [오버나이트 에이전트 플릿(Overnight Agent Fleet) 구축 체크리스트](https://tech.hancom.com/overnight-agent-fleet/)
- 회사: 한글과컴퓨터
- 본문 요약: 격리된 자율 에이전트를 병렬로 운영하고 사람은 결과를 검토·승인하는 플릿 모델을 설명합니다. 반복 업무부터 30·60·90일 단위로 검증하며 거버넌스와 지식 베이스를 구축해야 한다고 제안합니다.
- 주목할 point: 사람의 역할을 실행이 아닌 검토·승인으로 옮기는 단계적 도입 로드맵
- keyword: #AI에이전트 #거버넌스 #자동화

## [1년 차 주니어의 AX 스토리: OS 동적 분석 로직 최적화](https://techblog.samsung.com/blog/article/104)
- 회사: 삼성전자
- 본문 요약: TV 운영체제 패키지의 실행 로그로 커버리지를 측정하는 동적 분석 로직을 다룹니다. 두 대형 패키지에서 60시간 이상 걸리던 분석 병목을 최적화한 사례입니다.
- 주목할 point: 60시간 이상 걸리던 분석 병목을 찾아 개선한 구체적 사례
- keyword: #AX #동적분석 #성능최적화 #TV

## [AX를 통한 전사 암호화 서비스의 운영 효율화와 보안성 강화](https://techblog.samsung.com/blog/article/103)
- 회사: 삼성전자
- 본문 요약: D-KMS 개인정보 암호화 서비스에 AX를 적용해 운영을 개선한 사례입니다. 운영 효율화와 보안성 강화, SDK 에러 원인 대응을 다룹니다.
- 주목할 point: 암호화 서비스 운영에서 SDK 에러 원인 대응까지 AI 활용을 확장한 점
- keyword: #AX #암호화 #KMS #보안

## [AI 에이전트를 위한 멀티모달 의사결정 모델 ‘Kanana-v-decide’ 오픈소스 공개](https://tech.kakao.com/posts/846)
- 회사: 카카오
- 본문 요약: AI 에이전트의 반복적인 판단 작업을 위한 멀티모달 모델 Kanana-v-decide를 공개했습니다. 문의 분류, 이미지 확인, 도구 선택 같은 다음 동작 결정에 초점을 맞춥니다.
- 주목할 point: 범용 대형 모델 대신 에이전트의 '다음 동작 결정'에 특화한 오픈소스 모델
- keyword: #Kanana #멀티모달 #AI에이전트 #오픈소스
