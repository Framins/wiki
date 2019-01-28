# Process & Thread

*Process* 中譯：進程、程序；*Thread* 中譯：線程、執行序。以下用英文說明

## Process

聊 Process 之前，先講一下 Program

Program 指的是程式碼。Program 執行後會產生 Process。Process 一定需要 RAM，因此 Program + RAM = Process。除此之外，Process 除了 Resource 外，也包括了一個以上的 Thread。Thread 則是 CPU 執行程式的最小單元，它也是一條獨立的程式碼序列 (Code sequence)


## Conclusion

以其他觀點看 Process & Thread

|  Term  |  Object-oriented  |  Docker  |  Rancher  |
|  ----  |  ---------------  |  ------  |  -------  |
|  Program  |  Class  |  Image  |  Service  |
|  Process  |  Object  |  Container  |  Container  |
|  Thread  |  Method  |  N/A  |  N/A  |

以物件導向的概念來說，它很像 Class；以 Docker 生態來說，它很像 Image；以 Rancher 來說，它很像 Service

## References

* http://huan-lin.blogspot.com/2013/04/csharp-notes-multithreading-1.html
