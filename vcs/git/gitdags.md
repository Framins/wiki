# Gitdags

[Gitdags](https://github.com/Jubobs/gitdags) 是一個畫 Git 示意圖的工具，它基於 Latex 實作。以下介紹 Mac 該如何使用它。

## 安裝 MacTex

方法很簡單，可以去[官網](http://www.tug.org/mactex/)載，或是用 Homebrew ：

    brew cask install mactex

## 安裝 Gitdags 外掛

先 clone Gitdags 專案，外掛是該專案下的 `.sty` 檔，把它複製到下面這個目錄即可，不存在可以自己建立：

    mkdir -p ~/Library/texmf/tex/latex/
    cp gitdags.sty ~/Library/texmf/tex/latex/

## 編輯 Latex 檔

開始 TeXShop 即可開始編輯，可以用的範例可以參考官網，可以按 Typeset 預覽結果

## 建立 PDF 檔

下指令建 pdf

    pdflatex some.tex

## 安裝 pdf2svg

    brew install pdf2svg

## 下指令轉 svg

    pdf2svg some.tex some.svg

## 下指令轉 png

    qlmanage -t -s 1000 -o . some.svg

## 參考資料

* https://blog.othree.net/log/2017/03/25/gitdags-git/
