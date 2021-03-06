

# 说明

docker compose一建部署的命令 Nginx Mysql uwsgi Django 环境，多应用版本。

主要用途是为了方便自己快速搭建应用环境。

脚本同时部署了2个Django应用， Book 对应的是 80端口， hos 对应的是8080端口。 



# 配置

```
                       
D:.
│  .env                      # 环境变量
│  docker-compose.yml		 # docker compose 主文件
│  LICENSE                   # 说明文档
│  README.md            
│
├─build
│  └─django
│          Dockerfile        # django环境build文件
│          requirements.txt  # django环境安装插件
│
└─work
    ├─components
    │  ├─mysql
    │  │  ├─config
    │  │  │      my.cnf     #mysql 配置
    │  │  │
    │  │  ├─data
    │  │  └─log
    │  ├─nginx
    │  │  ├─config
    │  │  │  │  nginx.conf  # nginx配置
    │  │  │  │
    │  │  │  └─conf.d
    │  │  │          localhost.conf
    │  │  │
    │  │  └─log
    │  │          access.log
    │  │          error.log
    │  │
    │  ├─redis
    │  │  │  redis.conf
    │  │  │
    │  │  └─data
    │  └─uwsgi
    │      │  book_uwsgi.ini  #sgi配置
    │      │  hos_uwsgi.ini
    │      │
    │      └─book
    └─wwwroot
        ├─book
        │  │  manage.py
        │  │
        │  └─book
        │          settings.py
        │          urls.py
        │          wsgi.py
        │          __init__.py
        │
        └─hos
            │  manage.py
            │
            └─hos
                    settings.py
                    urls.py
                    wsgi.py
                    __init__.py

```

# 部署

1、根据拷贝的环境修改`.env`变量。

2、使用docker命令部署

>  docker-compose up -d #后台运行

# 配置说明：

redis 登录密码 123， 端口6379

mysql 用户名 root 密码 root 端口3306

Book 对应的是 80端口 

hos 对应的是  8080端口

# 额外的动作

1、 需要进入mysql配置中，创建datebase

> create database book
>
> create database hos

2、 Django 迁移数据库

>python manage.py makemigrations && python manage.py migrate

3、 Django 创建超级用户

> python manage.py createsuperuser

