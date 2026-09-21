# Docker Swarm Auto Scaling

AWS Cloud School 프로젝트 · 2026.02–03 · 3인 팀

Docker Swarm 환경에서 CI/CD, 자동 확장, 모니터링의 반응과 운영상 trade-off를 비교한 프로젝트입니다.

## My contribution

- CI/CD 구성, Shell·Prometheus 기반 자동화, 실험 설계와 수행을 담당했습니다.
- EC2 3대 환경에서 Shell·Prometheus 방식과 CloudWatch·SNS 방식의 scale-out 반응을 비교했습니다.
- 4개 조건을 각 10회씩 반복해 관측 결과를 확인했습니다.

## Repository guide

| Path | Purpose |
| --- | --- |
| `.github/workflows/deploy.yml` | GitHub Actions 기반 빌드·ECR 푸시·Swarm 배포 |
| `autoscale.sh` | Prometheus 지표 기반 서비스 확장 자동화 |
| `prometheus.yml` | Prometheus 수집 구성 |
| `dashboard-design.md` | Grafana 대시보드 설계 |
| `measurement-plan.md` | 반복 실험 계획 |

## Security configuration

- 배포 워크플로는 장기 AWS 액세스 키 대신 GitHub Actions OIDC를 사용합니다.
- 실행 전 GitHub Actions 변수 `AWS_ROLE_TO_ASSUME`에 OIDC 신뢰 관계가 구성된 IAM Role ARN을 등록해야 합니다.
- SSH 호스트와 개인 키는 각각 `MANAGER_IP`, `MANAGER_SSH_KEY` GitHub Secret으로만 관리합니다.
- `web.yml`의 ECR Registry와 Image Tag는 배포 시 환경변수로 주입되며, 실제 계정 식별자는 저장소에 기록하지 않습니다.

> 이 공개 저장소에는 실제 계정 ID, 접근 정보, 비밀값을 포함하지 않습니다.
