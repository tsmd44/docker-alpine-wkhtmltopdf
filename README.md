# docker-alpine-wkhtmltopdf

binaryの取り出し

```sh
$ id=$(docker create tsmd44/wkhtmltopdf)
$ docker cp $id:/bin/wkhtmltopdf - > wkhtmltopdf
$ docker cp $id:/bin/wkhtmltoimage - > wkhtmltoimage
$ docker rm -v $id
```

Multi stage build

```Dockerfile
...

From tsmd44/wkhtmltopdf as wkhtmltopdf


From php:7.2-fpm-alpine as base

COPY --from=wkhtmltopdf /bin/wkhtmltopdf /usr/local/bin/wkhtmltopdf
COPY --from=wkhtmltopdf /bin/wkhtmltoimage /usr/local/bin/wkhtmltoimage

...
```
