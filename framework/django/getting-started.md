Getting Started
===============

Docker
------

[Docker Hub 官方的 images](https://registry.hub.docker.com/u/library/django/)

可以直接用 onbuild image

```dockerfile
FROM django:onbuild
```

然後 build 的時候，除了 copy 程式外，另外會執行下列東西：

```dockerfile
RUN pip install
EXPOSE 8000
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

最後再執行 docker 即可

```bash
docker build -t django-app .
docker run --name django-app-1 -p 8000:8000 -d django-app
```

如果想用 docker 建 django 專案的話，用基本 image ：

```bash
docker run -it --rm --user "$(id -u):$(id -g)" -v "$PWD":/usr/src/app -w /usr/src/app django django-admin.py startproject mysite
```
