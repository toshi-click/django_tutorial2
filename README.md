# django_tutorial2
https://qiita.com/Gattaca/items/77cf379bcc99f1b8b324

## djangoの生成
```bash
docker-compose build
docker-compose run web_django django-admin startproject config .
```

## データベースの作成
```bash
docker-compose run web_django python3 manage.py migrate
```

## 全部をきちんと整理しておくため、プロジェクトの中に別のアプリケーションを作ります。
```bash
docker exec -it web_django python3 manage.py startapp restapi
```
rest_frameworkとrestapiというアプリを使うことをDjangoに知らせるためにsettings.pyのINSTALLED_APPSに追記します。
```
INSTALLED_APPS = (
    ...
    'rest_framework',
    'restapi.apps.RestapiConfig',
)
```

### モデルを作ったあとに
```
docker exec -it web_django python3 manage.py makemigrations restapi
docker exec -it web_django python3 manage.py migrate restapi
```

# 管理画面のスーパーユーザーの作成
```
docker exec -it web_django python3 manage.py createsuperuser
```

### Django Shell
```
docker exec -it web_django python3 manage.py shell
```

### サーバー上の静的ファイルの更新
```
docker exec -it web_django python3 manage.py collectstatic
```

### モデル追加後にテーブル作成
```bash
docker exec -it web_django python3 manage.py makemigrations restapi
docker exec -it web_django python3 manage.py migrate restapi
```