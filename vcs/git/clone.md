# git clone

用法如下：

    git clone <URI> <資料夾>

實際做的事如下：

    mkdir <資料夾>
    cd <資料夾>
    git remote add origin <URI>
    git fetch
    git pull origin master
