Promises 承诺，你将会得到延期或长期运行任务的未来结果。承诺有两个渠道：第一个为结果，第二个为潜在的错误。要获取结果，您将回调函数作为 then 函数参数。要处理错误，您将回调函数提供为 catch 函数参数。

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
</head>

<body>
    <script type="text/javascript">
        let p = new Promise((resolve, reject) => {
            setTimeout(function() {
                const result = Math.random();
                result > 0.5 ? resolve(result) : reject('Lower than 0.5');
            }, 2000);
        });

        p.then(result => {
            console.log('success', result);
        }).catch(result => {
            console.log('fail', result);
        });
    </script>
</body>

</html>
```



