Dockerfile
==========

Sample
---
- [username definition](https://github.com/jboss-dockerfiles/base/blob/master/Dockerfile)
- [runtime installation](https://github.com/jboss-dockerfiles/wildfly/blob/master/Dockerfile)
- [Use the environment variables to retrieve from outside the container](https://github.com/docker-library/postgres/blob/443c7947d548b1c607e06f7a75ca475de7ff3284/9.5/docker-entrypoint.sh)

FAQs
---

### CMD 與 ENTRYPOINT 的差別
> CMD 是 `docker run` 的 default command

### CMD 與 ENTRYPOINT 搭配使用
> https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact

### ADD 與 COPY 的差別
> ADD 與 COPY 功能相似, 只是 ADD 多了下面兩個功能
> - ADD allows `<src>` to be an URL
> - If the `<src>` parameter of ADD is an archive in a recognised compression format, it will be unpacked


Multiprocess in Docker container
---

* Supervisord
* S6 ([參考文章](http://kfei.logdown.com/posts/245469-using-s6-as-the-init-process-for-muliple-service-docker-container))

References
----------

* CMD 與 ENTRYPOINT 的差別參考: [Dockerfile最佳实践（一）](http://dockone.io/article/131)
* [Guidance for Docker Image Authors](http://www.projectatomic.io/docs/docker-image-author-guidance/)
