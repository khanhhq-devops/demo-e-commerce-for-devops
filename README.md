🚀 E-Commerce CI/CD Pipeline Project

Dự án xây dựng hệ thống CI/CD hoàn chỉnh cho ứng dụng e-commerce với monitoring và alerting tự động.

📋 Tổng quan
Dự án demo quy trình DevOps end-to-end bao gồm tự động hóa build, deploy, rollback và giám sát hệ thống thời gian thực. Mục tiêu đảm bảo code chất lượng được deploy nhanh chóng, an toàn và có thể rollback khi cần.

🔄 CI/CD Flow chi tiết
GitLab CI — Staging
Tự động chạy khi push code lên nhánh staging:

Build: build docker image frontend + backend

print notification: gửi thông báo về telegram quá trình deploy

release: push image lên Container registry(Harbor)

deploy: deploy lên staging-server

showlog: hiển thị log container sau khi deploy

Gilab CI - Production
Chỉ thực hiện sau khi satging ổn định:

Build: build docker image frontend+backend

Push: push image lên repo registry (Harbor)

Jenkins - Staging
Start: deploy lên môi trường staging-server
Stop: dừng các container đang chạy
Upcode: deploy version mới lên môi trường staging
Rollback: quay về version cũ từ backup.tar
Rollback hoạt động: mỗi lần upcode Jenkins tạo file backup.tar kèm timestamp. Khi rollback chỉ cần chọn file backup tương ứng và restore lại.

Jenkins - Production:
Start: deploy lên môi trường production-server
Stop: dừng các container đang chạy


📊 Monitoring & Alerting
Prometheus và Node Exporter cài trên production server thu thập metrics hệ thống. Grafana hiển thị dashboard trực quan. Alert gửi tự động qua Telegram.

Ngưỡng cảnh báo: 

CPU Usage > 80% -> alert: Telegram

RAM Usage > 85% -> alert: Telegram

Disk Usage > 90% -> alert: Telegram


🛠️ Tech Stack

Frontend: React/Vue

Backend: Node.js/Express

Database: MongoDB

Container: Docker

CI pipeline: Gitlab CI

CD pipeline: Jenkins

Monitoring: Prometheus+Grafana

Alerting: Telegram Bot

⚙️ Hướng dẫn cài đặt

Yêu cầu:

Docker & Docker compose

Gitlab account

Jenkins server

Telegram Bot Token + Chat ID


Các bước chạy:

1.Clonee repository

git clone https://github.com/khanhhq-devops/demo-e-commerce-for-devops.git

cd demo-e-commerce-for-devops

2.Cấu hình biến môi trường
cp backend/.env.development backend/.env
cp frontend/.env.development frontend/.env

3.Cấu hình Gitlab Ci Variables

Vào gitlab->settings->CI/CD->variables, thêm:

DOCKER_REGISTRY: URL container registry

REGISTRY_USER: Username registry

REGISTRY_PASSWORD: password regitry

STAGING_SERVER: IP staging-server

TELEGRAM_TOKEN: Bot token Telegram

TELEGRAM_CHAT_ID Chat ID telegram


4.Cấu hình Jenkins

Cài plugin Docker Pipeline

Cấu hình credentials registry

Tạo pipeline từ jenkins-parameters-staging và jenkins-parameters-production

5. Cài Node exporter trên production
wget https://github.com/prometheus/node_exporter/releases/download/v1.10.2/node_exporter-1.10.2.linux-amd64.tar.gz

tar xvf node_exporter-*.tar.gz

sudo cp node_exporter-*/node_exporter /usr/local/bin/

sudo systemctl enable --now node_exporter



🎯 Những gì học được từ project|

Xây dựng CI/CD pipeline hoàn chỉnh end-to-end

Phân biệt và phối họp Gitlbac CI và jenkins trong cùng 1 hệ thống

Triển khai monitoring với Prometheus+grafana

Thiết lập alerting tự động qua Telegram


👨‍💻 Tác giả

Hoàng Quốc Khánh

GitHub: https://github.com/khanhhq-devops

Email: khanhhoangg0106@gmail.com



