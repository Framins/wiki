MAC
===

Homebrew 管理器

http://homebrew-file.readthedocs.io/en/latest/index.html

---

MacOS 冷知識

開關動畫效果
-------

### Mission Control

打開

    defaults delete com.apple.dock expose-animation-duration;killall Dock

關閉

    defaults write com.apple.dock expose-animation-duration -int 0;killall Dock

### Launchpad

打開

    defaults delete com.apple.dock springboard-show-duration
    defaults delete com.apple.dock springboard-hide-duration;killall Dock

關閉

    defaults write com.apple.dock springboard-show-duration -int 0
    defaults write com.apple.dock springboard-hide-duration -int 0;killall Dock

版面
    
    defaults write com.apple.dock springboard-rows -int 6
    defaults write com.apple.dock springboard-columns -int 8;killall Dock
     
重排App順序
   
    defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock


References
----------

* http://www.macgg.com/archives/6395.html
