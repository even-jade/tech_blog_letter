<!-- 이 파일은 posts/2026-10-18.md의 사본입니다. 자동 생성됨. -->
# 2026-10-18 기술 블로그 모음

## [AWS에서 AI 에이전트 실행 환경 격리하기 1부: Amazon EKS와 Agent Sandbox, 개념과 구성](https://aws.amazon.com/ko/blogs/tech/aws-ai-agent-sandbox-eks-isolation-part-1/)
- 회사: AWS
- 본문 요약: Kubernetes SIG Apps의 Agent Sandbox v1.0.5와 gVisor를 EKS 1.36에 구성하고, 모델이 생성한 신뢰할 수 없는 코드를 막는 격리 계층을 runc와 gVisor로 비교했습니다. Sandbox·SandboxTemplate·Warm Pool·SandboxClaim 리소스 구조와 설치 순서(gVisor 전용 Managed Node Group, RuntimeClass, VPC CNI NetworkPolicy 활성화, 컨트롤러·sandbox-router 설치)를 설명합니다. 동일 점검 스크립트(/etc/shadow 읽기, setuid(0), ServiceAccount 토큰 읽기) 결과, 4개 항목 중 3개는 gVisor가 아닌 PodSpec 보안 설정과 컨트롤러 기본값이 막았고 gVisor는 호스트 커널 노출을 줄이는 역할을 했습니다.
- 주목할 point: EKS Auto Mode는 runsc 등록이 불가능해 Managed Node Group이 필요하고, VPC CNI NetworkPolicy를 켜지 않으면 템플릿의 정책이 적용되지 않습니다. gVisor를 도입해도 Pod 보안 설정(비루트, capability 제거 등)은 그대로 갖춰야 합니다.
- keyword: #AgentSandbox #gVisor #EKS #Kubernetes #AI에이전트 #보안

## [AWS에서 AI 에이전트 실행 환경 격리하기 2부: Amazon EKS와 Agent Sandbox, 개념과 구성](https://aws.amazon.com/ko/blogs/tech/aws-ai-agent-sandbox-eks-isolation-part-2/)
- 회사: AWS
- 본문 요약: 운영 환경 적용 시 확인할 사항을 측정 결과와 함께 다룹니다. NetworkPolicy 활성화 전후 비교(메타데이터·K8s API 차단), 기본 DNS 주입(8.8.8.8)을 Route 53 Resolver로 바꾸는 사용자 정의 정책, Warm Pool 사용 시 Claim→Ready가 약 2초에서 약 55ms로 단축(Cold Start 대비 34~36배), Pod IP 재사용 대기(30초)로 인한 burst 지연, gVisor의 시스템 콜 비용(2~12배), 만료·일시 중지·EBS 상태 보존, Bedrock의 Claude 에이전트 연동, sandbox-router 인증·접근 제한을 설명합니다.
- 주목할 point: 기본 정책은 인터넷 egress를 모두 허용하므로 외부 통신은 egress 프록시·Network Firewall 등으로 따로 통제해야 합니다. 에이전트와 샌드박스의 역할 분리는 네트워크가 아니라 자격 증명 계층에서 성립하며, router는 기본 allow-all이고 port-forward는 NetworkPolicy를 우회하므로 RBAC 제한이 필요합니다.
- keyword: #AgentSandbox #WarmPool #NetworkPolicy #VPCCNI #sandbox-router #Bedrock

## [AWS Direct Connect 정액 요금제(Flat-rate) 손익분기점 분석](https://aws.amazon.com/ko/blogs/tech/aws-direct-connect-flat-rate-breakeven-analysis/)
- 회사: AWS
- 본문 요약: 2026년 9월 출시된 10/100 Gbps 전용 연결의 정액 요금제를 서울 리전 10 Gbps 연결 2개(20 Gbps) 기준으로 분석합니다. Tier 1 정액 요금은 포트페어 1쌍 월 8,154.24 USD, 독립 연결 2개 월 16,308.48 USD이며, 손익분기 월 DTO는 각각 약 114 TB(평균 376 Mbps)와 약 309 TB(평균 1.01 Gbps)입니다. 가상 청구서(종량제 80,052.47 USD) 대비 절감률은 89.81%와 79.63%입니다.
- 주목할 point: 포트페어의 사용 가능 용량은 포트 1개 분량(10 Gbps)이라는 점, Tier 범위 밖 DTO·Transit Gateway 처리 요금은 별도라는 점, 같은 로케이션 연결은 같은 요금제여야 하고 6개월 3회로 변경이 제한된다는 점을 전환 전에 확인해야 합니다.
- keyword: #DirectConnect #정액요금제 #비용최적화 #손익분기점 #네트워킹
