# Project Directory Structure

專案裡面預設的目錄結構如下

| Files | Description |
| ----- | ----------- |
| `config.ru` | 用來啟動應用程式的 Rack 伺服器設定檔 |
| `Gemfile` | 定義此專案要使用哪些 Gems 套件 |
| `README.md` | 說明 |
| `Rakefile` | 載入可以被命令列執行的一些 Rake 任務 |
| `app/` | 程式主要內容都放在這個目錄，包括 MVC 檔案 |
| `app/controllers/` | 控制器 |
| `app/helpers` | Helpers |
| `app/models` | Models |
| `app/views` | Views |
| `config/` | 設定檔、路由、資料庫設定 |
| `db/` | 資料庫的結構綱要 |
| `doc/` | 用來放自己看的文件 |
| `lib/` | 放一些自定的 Module 和類別檔案 |
| `log/` | 應用程式的 Log 記錄檔 |
| `public/` | 網路上看得到的目錄，css js 圖檔等靜態檔都是放這裡 |
| `script/` | 放 rails 指令和其他 script 指令 |
| `test/` | 放單元測試 |
| `tmp/` | 暫存檔 |
| `vendor/` | 用來放第三方程式碼外掛的目錄 |
