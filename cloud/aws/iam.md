AWS Identity and Access Management (IAM)
========================================

簡稱 [IAM](https://aws.amazon.com/tw/iam/)

IAM 有四個部分

* Group
* User
* Role
* Policy

### Group

Group 裡可以加入多個 User 和這個 Group 可以用的 Policy

### User

User 可以定義虛擬的操作者名稱，通常是定義 AP 要登入的帳號

### Role

Role 是定義真實人類要使用的帳號

### Policy

Policy 是定義 Group / User / Role 能使用 AWS 的哪些 Service 或是 Service 下的 Resource ，或是操作的權限
