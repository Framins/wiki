# Amazon Virtual Private Cloud

簡稱 [Amazon VPC](https://aws.amazon.com/tw/vpc/)

VPC 的四種模式

1. Public Subnet
2. Public + Private Subnet
3. VPN + Public + Private Subnet
4. VPN + Private Subnet

關鍵差別如下

* 123 都有提供公開服務給外面使用；4 則沒有
* 12 是公有雲；3 是混合雲；4 是私有雲
* 1 跟 2 的差別為，2 的某些服務是不對外公開的

## Keyword

* Subnet
* Internet Gateway
* NAT Gateway - 需指定 Subnet
* Route table
* Security Group - 來源可以是 Security Group ID

### ACL

* Subnet Layer Firewall
* Stateless Firewall
* 編號設定優先順序，越低越優先
* 符合規則就會進行動作
* Subnet 只能也一定會 associate 一個 ACL

### Security Group

* Host Layer Firewall
* Stateful Firewall
* 只能設定 Allow
* Security Group 可以 attach 給無限多個
* 每個 ENI 只能設定 5 個 Security Group

## References

* [AWS雲服務的進階安全措施－VPC (Virtual Private Cloud)](http://www.tts.bz/archives/1488)
* [AWS VPC 設定教學](http://blog.yslin.tw/2014/02/aws-vpc.html)
