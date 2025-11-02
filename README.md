🚀 AWS Fargate PoC — Node.js CI/CD Architecture

Bu proje, Node.js tabanlı bir web uygulamasını tam otomatik CI/CD hattı ile AWS üzerinde serverless container olarak çalıştırmak için hazırlanmıştır.

⚙️ Amaç

Kod değişiklikleri GitHub üzerinden push edildiğinde:

GitHub Actions pipeline otomatik olarak tetiklenir.

Yeni Docker imajı oluşturulur ve ECR’a push edilir.

ECS’deki Task Definition güncellenir.

Yeni sürüm Fargate üzerinde otomatik olarak deploy edilir.

🧩 Mimari Bileşenler
🧑‍💻 Developer Flow

Git Push (main branch)
Kod push edildiğinde GitHub Actions otomatik çalışır.

⚙️ CI/CD Katmanı — GitHub Actions

Checkout source

Configure AWS credentials

Build Docker image

Push image to Amazon ECR

Register new ECS Task Definition Revision

Update ECS Service & Force New Deployment

☁️ AWS Networking & Security

CloudFront: CDN + SSL + Cache yönetimi

AWS WAF: Web Application Firewall koruması

ALB (Application Load Balancer): Trafik dağıtımı

Target Group: Health check ve trafik yönlendirmesi

VPC: Tüm kaynakları kapsayan özel ağ

Security Groups

NAT Gateway

VPC Endpoints (ECR / S3 erişimi)

🧱 AWS Infrastructure

ECS Fargate Service: Container’ı çalıştıran serverless compute servisi

Container: Node.js uygulaması

RDS MySQL: Uygulamanın veritabanı bağlantısı

🔍 Health Check

ALB’nin health check endpoint’i /health olarak tanımlanmıştır.

Eğer container veya RDS bağlantısı başarısız olursa, ECS task otomatik olarak yeniden başlatılır.

📊 CloudWatch + SNS Monitoring

CloudWatch metrikleri: CPUUtilization, MemoryUtilization

SNS Notification: CPU %1’i geçtiğinde e-posta bildirimi gönderilir.

Alarm threshold’ları ileride composite alarm yapısına dönüştürülebilir.

🧠 Teknoloji Yığını

Node.js / Express.js

AWS ECS Fargate

AWS ECR

AWS CloudFront

AWS ALB + WAF

AWS RDS (Aurora MySQL)

AWS CloudWatch + SNS

GitHub Actions (CI/CD)

🖼️ Mimarinin Görseli

🧾 Notlar

.env dosyası .gitignore içinde gizlenmiştir.

ALB health check /health endpoint’ine bakar.

CloudWatch alarmları manuel veya otomatik tetikleme için kullanılabilir.