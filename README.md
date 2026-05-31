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
Start: 
