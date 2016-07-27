# zf Command Line Tool

設定zf命令列工具

## Setup

### Debian Series

直接下指令安裝

    apt-get install zend-framework-bin

安裝好後，就可以直接使用 `zf` 了

### Mac OSX

可以直接用alias指定，另外記得要加執行權限才能執行。

    # use Zend Server
    alias zf=/usr/local/zend/share/ZendFramework/bin/zf.sh
    chmod +x /usr/local/zend/share/ZendFramework/bin/zf.sh

另一種方法是直接建立zf的連結到系統的預設執行路徑

    ln -s /usr/local/share/ZendFramework/bin/zf.sh /usr/local/bin/zf
    chmod +x /usr/local/bin/zf

## Usage

使用方法

### Help

基本查詢說明

    zf --help

查詢特定的關鍵字說明

    zf ? [keyword]

### DbAdapter

線上查詢

    zf ? dbadapter

語法

    zf configure dbadapter [DSN] [Section=production]

設定 `DbAdapter` ，假設資料庫資訊如下：

* adapter: Pdo_Mysql
* username: username
* password: password
* dbname: database

可以下此指令：

    zf configure dbadapter "adapter=Pdo_Mysql&username=username&password=password&dbname=database"

> DSN 用雙引號包起來比較保險

假設是 SQLite ：

    zf configure dbadapter "adapter=Pdo_Sqlite&dbname=../data/database.db"

它也可以針對特定的設定檔區塊新增設定

    zf configure dbadapter "adapter=Pdo_Sqlite&dbname=../data/database.db" development
    zf configure dbadapter "adapter=Pdo_Sqlite&dbname=../data/database.db" testing

### DbTable

線上查詢

    zf ? dbtable
    zf create db-table.?

語法

    zf create db-table [name] [actual-table-name] [module]
    zf create db-table.from-database [module]

* `name` 是 class 和檔案名稱
* `actual-table-name` 是實際資料庫裡面的 table name
* `module` 是 module name
* `--force-overwrite` 可以強制覆蓋原有的檔案

範例

    zf create dbtable User user --force-overwrite

它也可以直接從 database 抓取資料並生成 DbTable class

    zf create dbtable.from-database

> 它會從 production 裡面的 database 設定裡抓
