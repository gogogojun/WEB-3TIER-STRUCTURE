# WEB 3-Tier Architecture with Terraform

## 📖 프로젝트 개요
AWS 상에서 **3-Tier 아키텍처(웹, 앱, DB 계층)**를 Terraform으로 구현한 프로젝트입니다.  
Auto Scaling, ALB, Aurora MySQL 등을 통해 확장성과 가용성을 갖춘 웹 애플리케이션 구조를 설계/실습했습니다.

---

## 🛠️ 아키텍처
<img width="601" height="801" alt="제목 없는 다이어그램 drawio" src="https://github.com/user-attachments/assets/5ae00e59-2f54-4407-bb08-757f21343fff" />

- **네트워크**
  - VPC, Public/Private Subnet, NAT Gateway, Route Table
- **보안**
  - Bastion Host (Public Subnet)
  - 보안 그룹 (ALB / EC2 / RDS 분리)
- **컴퓨팅**
  - Auto Scaling Group (EC2 * 2, Private Subnet)
  - User Data Script → Apache + PHP + DB 연동
- **로드 밸런싱**
  - Application Load Balancer(ALB) + Target Group + Listener
- **데이터베이스**
  - Amazon Aurora MySQL (Writer + Reader, Multi-AZ)



## 📂 폴더 구조
```plaintext
WEB-3tier-Structure/
├── VPC.tf
├── instances.tf
├── userdata.sh
├── ELB.tf
├── RDS.tf
└── terraform.tf
```




## ⚙️ 동작 흐름
1. `terraform init` → provider 초기화
2. `terraform plan` → 리소스 생성 계획 확인
3. `terraform apply` → VPC, EC2, ALB, RDS 등 자동 생성
4. ALB DNS 주소로 접속 → 웹서버 페이지 확인
5. Bastion Host를 통해 RDS 접속 및 테이블 데이터 검증



## ✅ 실행 결과
- ALB DNS 접속 → 웹 페이지 정상 출력
- Bastion Host를 통한 RDS 접속 및 테이블 검증 완료
- Auto Scaling 그룹에 의해 EC2 인스턴스 자동 관리
