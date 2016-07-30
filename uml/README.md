UML
===

Unified Modeling Language ，統一塑模語言

* Structure diagrams
  * Static diagrams
    * [Class Diagram](class-diagram.md)
    * Object Diagram
    * Package Diagram
  * Implementation diagrams
    * Component Diagram
    * Deployment Diagram
  * Profile Diagram
  * Composite Structure Diagram
* Behavior diagrams
  * Activity Diagram
  * State Machine Diagram
  * Use Case Diagram
  * Interaction diagrams
    * Communication diagram
    * Interaction overview diagram
    * Sequence diagram
    * Timing Diagram

Tools
-----

http://wind13.lofter.com/post/b2b9b_fda5d7

  * [PlantUML](http://plantuml.sourceforge.net/index.html)
  * [CodeUML](http://www.codeuml.com/)

### Installation

PlantUML 太好用了，以這個做說明

#### Dokuwiki

1. 安裝 [plantuml Plugin](https://www.dokuwiki.org/plugin:plantuml)
2. 安裝 JVM
3. 安裝 [graphviz](http://www.graphviz.org/)
4. 下載 [plantuml.jar](http://plantuml.sourceforge.net/download.html)
5. 到系統設定 java 和 jar 的位置，改成 Local render
6. Done

中文字體需要另外裝，不然會出現亂碼...  

    apt-get install ttf-wqy-zenhei
    fc-cache -v

#### IntelliJ IDEA

1. 安裝 [plugin](https://plugins.jetbrains.com/plugin/7017)
2. 安裝 [graphviz](http://www.graphviz.org/)
3. Done
