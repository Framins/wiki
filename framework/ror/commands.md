# Commands

新增 Controller 的指令為：

    rails g controller [ControllerName] [MethodName]

Method 可以不打，也可以打很多個，如：

    rails g controller todo index new create show edit update destroy

如果沒打 Method 的話，就不會自動建立 `router` 規則和 `erb` 樣板檔，有打則一個 method 都會自動新增一個規則和一個樣板檔。
