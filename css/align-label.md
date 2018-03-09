```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>
    <style>
        p {
            position: relative;
            width: 5em;
            text-align: justify;
            text-align-last: justify;
        }

        p:after {
            content: ":";
            position: absolute;
            right: -6px;
        }
    </style>
</head>

<body>
    <p>你好</p>
    <p>我爱中国</p>
    <p>我是谁</p>
</body>

</html>

```



