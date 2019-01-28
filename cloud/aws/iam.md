AWS Identity and Access Management (IAM)
========================================

簡稱 [IAM](https://aws.amazon.com/tw/iam/)

權限集中管理的地方，IAM 有四個部分

* Group
* User
* Role
* Policy 可以限制 Entity (即上述三者) 存取 AWS Resource

Some practices

* 移除 root account 的 key，只靠 console 看 billing
* 啟動密碼規則並啟動 MFA
* 建立帳號要 Mapping 特定人，並做最小權限原則
* 群組設定權限
* EC2 用 Role
* Static credential 定期換
* 使用 CloudTrail 稽核 account 活動記錄

### Group

Group 裡可以加入多個 User 和這個 Group 可以用的 Policy

### User

User 是定義真實人類要使用的帳號

新建 AWS User 不具有任何權限，建議去使用群組來 attach policy，預設可以加入 10 個 group

建 account 建議要設定密碼原則，如長度、組成、期限、重複使用限制等

### Role

Role 可以定義虛擬的操作者名稱，通常是定義 AP 要登入的帳號

### Policy

Policy 是定義 Group / User / Role 能使用 AWS 的哪些 Service 或是 Service 下的 Resource，或是操作的權限

格式為 JSON，每個 entity 只能套用最多 10 個 Policy

Policy 有明確說 Deny，則 Deny 優先

順序為：

* Explicit Deny
* Explicit Allow
* Default Deny
