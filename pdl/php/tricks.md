Tricks
======


Git Hook
--------

編輯檔案 `/path/to/project/.git/hooks/pre-commit` ，並加上執行權限

行為如下

1. 修改檔案並 add
2. `files` 變數會存著準備要 commit 的 php 檔
3. 執行 unit test
4. 對步驟 2 的檔案做 coding style 檢查
5. 最後如果失敗即會報錯，正常就會進入 commit 畫面

```bash
#!/bin/sh
# Run PHP validation before commit
#
# Ensure installed extensions below:
#     squizlabs/php_codesniffer~2.6.2
#     codeception/codeception~2.2.3

# get all file which will commit
files=$(git diff --cached --name-only --diff-filter=ACM | grep ".php$")
pass=true

# run unit test
echo ">>> Running Unit Test"
php vendor/bin/codecept run unit --report --silent

if [ "$?" != "0" ]; then
    pass=false
fi

echo ">>> Unit Test finished"

# run code sniffer
echo ">>> Running Code Sniffer"

if [ "$files" != "" ]; then
    for file in ${files}; do
        # 因為 codeception 的 test code style 跟 PSR2 差蠻多的，所以先忽略
        if [ "${file%%\/*}" != "tests" ]; then
            php vendor/bin/phpcs --standard=PSR2 ${file};

            if [ "$?" != "0" ]; then
                pass=false
            fi
        fi
    done
fi

echo ">>> Code Sniffer finished"

# result
if $pass; then
    exit 0
else
    echo ""
    echo "COMMIT FAILED!!"
    exit 1
fi
```

### Add Composer Scripts

配合 git repo 和 [composer scripts](https://getcomposer.org/doc/articles/scripts.md#command-events) 可以偷偷導入 CI 最開始的檢查機制

首先先把檔案放在 `/path/to/project/scripts/pre-commit`

> 位置是個人習慣，也有人叫 `hooks` ，放哪都可以

接著 `composer.json` 修改 scripts 如下

```json
{
    "scripts": {
        "post-install-cmd": [
            "php -r \"copy('scripts/pre-commit', '.git/hooks/pre-commit');\""
        ]
    }
}
```
