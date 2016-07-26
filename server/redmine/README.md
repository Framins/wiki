# Redmine

Redmine 為一個結合專案管理 (Project management) 和缺陷跟蹤管理系統 (Issue tracking system) 的管理系統，對程式設計員來說，還有更大的優點在於它有版本控制系統，更不用提它還是開放原始碼軟體。

唯一缺點就是，通常都會在建構上遇到重重困難。

基本功能

* Project task management : 專案的工作項目管理
* Issue tracking system : 專案功能臭蟲的進度追蹤管理
* Project status tracking : 專案狀態管理
* Human resource management : 專案人力資源管理
* Project information sharing : 專案資訊的共享平台
* Source code control integrated : 整合SCM系統
* Code review: 程式碼檢討 (透過Plugin 達成)
* Project documents management: 專案文件管理

特點

* Multiple projects support: 支援多個專案
* Flexible role based access control: 可以自己定義角色與權限
* Flexible issue tracking system: 彈性化的 Issue 追蹤管理
* Gantt chart and calendar: 甘特圖和行事曆的支援
* News, documents & files management: 新聞, 檔案與文件的管理
* Feeds & email notifications: 自動通知機制
* Per project wiki Per project forums: 支援 Wiki , 論壇
* Time tracking: 時程追蹤管理
* Custom fields for issues, time-entries, projects and users: 客制化欄位
* SCM integration (SVN, CVS, Git, Mercurial, Bazaar and Darcs): SCM 整合
* Issue creation via email: 透過Email新增Issue
* Multiple LDAP authentication support: 支援各式 LDAP
* User self-registration support: 支援使用者自己註冊帳號
* Multilanguage support: 多國語言支援
* Multiple databases support - (SQLite、MySQL、PostgreSQL): 支援多種資料庫
* Code review: 程是碼檢討

使用Redmine 的另個好處是可以幫助 ISO, PMP, CMMI 的推動.因為它可以涵蓋許多的範圍:

* ISO: 你可將所有ISO定義的文件, 使用 Redmine 來管理, 另外他所定義的流程 (通知, 審核, 備份) 在 Redmine上 都可達成.
* PMP: PMBOK9 所定義的九大 Knowledge area, Redmine mine 可以涵蓋其中六項: Integration Management , Scope Management , Time Management, Quality Management, Human Resource Management, Communications Management. 並部份涵蓋到其中兩項: Cost Management, Risk Management.
* CMMI: 在CMMI Level1~5 所定義的Process area 中, 他可以涵蓋到其中十項: MA, CM, PP, PMC, PPQA, REQM, IPM, DAR, OPF, OPD. 並部分涵蓋到三項: RSKM, OPP, QPM.

使用Redmine有幾點要注意:

* 要設計好你的組織與專案人員架構,
* 根據你的架構, 使用者, 角色, 設定好相關權限
* 設定好各式 Tracker (Bug, Feature, Support, Code revew等) 也就是你要追蹤管理的標的, 以及他的狀態 (Status) 與流程 (WorkFlow)
* 做好教育訓練, 讓使用者充分了解你所定義的流程與角色
* 督促使用者詳實紀錄各自的工作狀況與結果.
* 定時檢討流程與改善

透過它你可以把整個軟體流成串接起來, 從專案開始:

* 專案人員的管理
* 專案範圍的定義
* 專案時程規劃, WBS 展開
* 工作項目追蹤
* 整合 SCM
* 臭蟲追縱管理
* 專案資訊分享
* 專案文件版本與權限管理
* 程式碼檢討
* 專案的Wiki製作
* 專案人員討論區
* 專案報表(甘特圖, 行事曆, 各種資料的統計報表)
* Image的發行版本管理
* 另外透過 PAM 模組, 還可以跟 SCM , 檔案系統 (FTP), KM 系統, 教育訓練系統做帳號的整合. 做到全方位的軟體專案管理. 有軟體專案管理困擾的團隊, 試著架構一套 Redmine 起來吧, 絕對能讓你的管理更加輕鬆寫意!

# Setup

* [Setup on Ubuntu](setup-on-ubuntu.md)
* [Setup on Heroku](setup-on-heroku.md)
