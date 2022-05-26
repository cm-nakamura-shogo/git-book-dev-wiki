# phpmyadmin

## docker

### WebUIのポート番号を変更する

* 環境変数がないため、以下のコマンドで設定ファイルを置換する。

```Dockerfile
RUN cat /etc/apache2/sites-available/000-default.conf \
    | sed -e 's#<VirtualHost \*:80>#<VirtualHost \*:8080>#g' \
    >/etc/apache2/sites-available/000-default.conf

RUN cat /etc/apache2/ports.conf \
    | sed -e "s#Listen 80#Listen 8080#g" \
    >/etc/apache2/ports.conf
```
