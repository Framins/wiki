# .gitignore for Laravel

預設的 Laravel 有 `.gitignore` 檔，以下是修改過後的範例:

```
# Composer files
vendor
composer.phar

# Default ignore file for Laravel
bootstrap/compiled.php
.env.*.php
.env.php

# Node modules
node_modules

# Global/Temp file
*~
*.swp

# Global/OSX.gitignore
.DS_Store

# Global/Windows.gitignore
Thumbs.db
Desktop.ini

# Thumbnails
._*

# Files that might appear on external disk
.Spotlight-V100
.Trashes

# NetBeans project files
nbproject/*

# IntelliJ IDEA project files
.idea
*.iml
```
