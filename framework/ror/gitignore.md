# .gitignore

預設用 rails 指令產出來就會有 `.gitignore` 檔了，以下是個修改過的範例：

```git
# Ignore bundler config.
Gemfile.lock
bin/
.bundle
vendor/bundle

# Ignore the default SQLite database.
db/*.sqlite3
db/*.sqlite3-journal

# Ignore all logfiles and tempfiles.
log
tmp

# Project
.rbenv-version
.rbx
.rvmrc
.ruby-version

# YARD
.yardoc
yardoc/
doc/

# Global/OSX.gitignore
.DS_Store

# Files that might appear on external disk
.Spotlight-V100
.Trashes

# Global/Windows.gitignore
# Windows image file caches
Thumbs.db
Desktop.ini
```
