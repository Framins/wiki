Amazon Web Services
===================

[Amazon Web Services](https://aws.amazon.com/)

一開始建立帳號會是 root 權限，建議會去 [IAM](iam.md) 建立一個 Group 指定權限後，再開一個 User 指定到該 Group ，另外也建議開啟兩階段認證登入。 AWS 是用 [Google Authenticator](https://www.google.com.tw/webhp#q=google%20authenticator) 做驗證。

## IDC 基礎設施

* **Avilability Zone:** 地理 100 公里以上
* **Regions:** 地理上大範圍的區域
* **Edge Locations:** Proxy

Regions 選法：不同的 Regions 會有不同的價格，像東京比較貴，可是東京比較近（ < 100ms ），所以除了基本需求外，還要考慮環境因素來選擇。

## AWS Credentials

* Account/Password/MFA - 人類登入使用
* Access key ID/Secret access key - 機器用
* Key Pair (EC2)

## 主要核心功能

* [Amazon Elastic Compute Cloud (Amazon EC2)](ec2.md)
* [AWS Lambda](https://aws.amazon.com/tw/lambda/)

### Storage

* [**Amazon Simple Storage Service (S3):**](https://aws.amazon.com/tw/s3/)
* **Glacier:** 備份需求會用到，檔案讀取需要數小時
* **Snowball:** 大檔傳送到 AWS 時可以用
* **Storage Gateway:** 提供一個空間，可以同步到 S3
* [Amazon Elastic Block Store (Amazon EBS)](https://aws.amazon.com/tw/ebs/)

### Database

* [**Amazon Relational Database Service (RDS):**](https://aws.amazon.com/tw/rds/) 強關聯資料用， MySQL, Oracle (也有提供 Master / Slave 服務)
* [**Amazon DynamoDB:**](https://aws.amazon.com/tw/dynamodb/) 高速存取用， Like Mongo
* **ElastiCache:** 使用 Cache 用， Memcached / Redis
* [**Amazon Redshift:**](https://aws.amazon.com/tw/redshift/)
* **DMS:** 搬移資料庫用

### Network

* [**Amazon Virtual Private Cloud (VPC):**](vpc.md) 可視為獨立的機房，在裡面的網路規劃都是可以自定義的，如子網域如何切
* **Direct Connect:** 可以拉專線到 AWS 機房，不過台灣用不到，因為沒機房
* **Route 53:** 就是 DNS

### Developer Tools

* **CodeCommit:** 就是 Git
* **CodeDeploy:** 就是 CI/CD
* **CodePipeline:**

### Management Tools

* **CloudTrail:** 可以追縱在 AWS 操作記錄
* **OpsWorks:** 可以定義一個流程

### Security & Identity

* [**AWS Identity and Access Management (IAM):**](iam.md)
* **Certificate Manager:** 管憑證

### Analytics

* **Elasticsearch Service:** 可以快速建立搜尋引擎

### Mobile Service

* **SNS:** push notification service

### Application Service

* **API Gateway:** 可搭配 Lambda
* [**Amazon Simple Queue Service (Amazon SQS):**](https://aws.amazon.com/tw/sqs/) Queue

## 核心擴充出來的功能

* [Amazon EC2 Container Registry (ECR)](https://aws.amazon.com/tw/ecr/)
* [Amazon EC2 Container Service (ECS)](https://aws.amazon.com/tw/ecs/)

## 輔助核心功能

* [Elastic Load Balancing](https://aws.amazon.com/tw/elasticloadbalancing/)

## 開發人員工具

* [AWS Tools](https://aws.amazon.com/tw/tools/)
* [AWS CLI](cli.md)

## References

* [Amazon雲端服務活用術](http://www.ithome.com.tw/article/88754)
* [常用的AWS服務](http://www.tts.bz/archives/2450)
