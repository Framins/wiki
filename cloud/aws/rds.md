# Amazon Relational Database Service

Multi-AZ RDS 是以 Active/Standby 模式運作
- Failover 需要3分鐘，可以手動強制切換
- 避免進行 snapshot / backup，IO 進入 suspend

Primary RDS 支援最多 5 個 Read Replica
- Async，由 Primary Instance 產生 Read Only Instance
- 可轉 RW RDS，但原本的 Replication 會停止
- Aurora 支援 15 個 Read Replica
