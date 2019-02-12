# Amazon Elastic Compute Cloud

簡稱 [Amazon EC2](https://aws.amazon.com/tw/ec2/)

預設 IP 是動態的，如果要用靜態的需要選 Elastic IPs

Warning: 這是要額外花錢的

EC2 的使用策略：壞了就重開，如果太常壞就要回 staging 階段檢查程式有無問題，再重新 deploy。

Note: 很像把 EC2 當作是 Container 處理一樣

## Options

* Reserver Instance
  + 保證機器隨要隨有
  + 簽約並付訂金，可以得到 30% ~ 70% 折扣
  + 不能跨 region，無法中途終止合約
* On-Demand Instance
  + 並不保證隨要隨有
  + 每小時收錢
  + 不滿一小時以一小時計
* Spot Instance
  + 競標方法取得 EC2
  + Bid Price 設定可接受的最高價格
  + 一般可以節省 50% ~ 90%

## References

* [Service for EC2 指定固定IP及釋放IP](http://jyeh-blog.logdown.com/posts/712216-aws-ec2-service-for-ec2-specifying-a-fixed-ip)
