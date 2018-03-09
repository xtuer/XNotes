使用 JODConvert 把 work 转为 pdf 或者 html 时需要后台启动 LibreOffice 服务:

* `./soffice --headless --accept="socket,host=127.0.0.1,port=2002;urp;"`

* `./soffice --headless --accept="socket,host=127.0.0.1,port=8100;urp;" --nofirststartwizard &`



