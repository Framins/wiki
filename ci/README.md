Continuous Integration
======================

Practice
--------

以下參考 Teddy 的文章

* [開發人員應遵循的七項持續整合要領](http://teddy-chen-tw.blogspot.tw/2012/07/blog-post.html)
* [持續整合工程師應遵循的十項要領（上）](http://teddy-chen-tw.blogspot.tw/2012/07/blog-post_04.html)
* [持續整合工程師應遵循的十項要領（下）](http://teddy-chen-tw.blogspot.tw/2012/07/blog-post_05.html)

Developer 應該了解的要點

1. Commit code frequently
2. Don’t commit broken code
3. Fix broken builds immediately
4. Write automated developers tests
5. All tests and inspections must pass
6. Run private builds
7. Avoid getting broken code

CI Engineer 應該了解的要點

1. Automate builds
2. Perform single command builds
3. Separate build scripts from your IDE
4. Centralize software assets
5. Create a consistent directory structure
6. Fail builds fast
7. Build for any environment
8. Use a dedicated CI machine and a CI server
9. Run fast builds
10. State builds

Implements
----------

* [GitLab CI](gitlab-ci.md) GitLab built-in Service
* [Pipelines](https://bitbucket.org/product/features/pipelines) Bitbucket built-in Service
* [Jenkins CI](http://jenkins-ci.org/)
* [Circle CI](circle-ci.md)
* [Travis CI](https://travis-ci.org/)
* [Drone.io](https://drone.io/)
* [TeamCity](https://www.jetbrains.com/teamcity/) JetBrains 家出的 CI
* [Codeship](https://codeship.com/) SaaS 服務，跟 [AWS](/cloud-computing/aws/README.md) 整合良好
* [Bamboo](https://www.atlassian.com/software/bamboo) Atlassian 家出的 CI
* [PHPCI](https://www.phptesting.org/)

其他好用的工具

* [Shields.io](http://shields.io/) - 用圖表示目前專案的健康度

Reference
---------

* [漫談持續整合](http://kojenchieh.pixnet.net/blog/post/378400769)
* [持續整合所需準備事項](http://kojenchieh.pixnet.net/blog/post/378870311)
* [執行持續整合所需要的紀律](http://kojenchieh.pixnet.net/blog/post/379112090)
* [十件有關CI的事情](http://kojenchieh.pixnet.net/blog/post/75411763)
* [內修敏捷開發心法 + 外練持續整合招式](https://blog.toright.com/posts/4139)
* [Git Workflows and Continuous Delivery](http://blogs.wandisco.com/2013/07/24/git-workflows-and-continuous-delivery-using-multisite-replication-to-facilitate-a-global-mainline/)
