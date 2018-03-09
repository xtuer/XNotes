```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <script src="http://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>
    <style media="screen">
        canvas {
            border: 1px solid grey;
            width: 500px; /* canvas 的渲染宽度 */
            height: 300px;
        }
    </style>
</head>

<body>
    <canvas id="canvas">Your browser does not support canvas.</canvas>

    <script>
        var canvas = $('#canvas').get(0);
        canvas.width = 500; // canvas 的实际宽度，默认是 300
        canvas.height = 300;
        var ctx = canvas.getContext('2d');

        ctx.beginPath(); // 方法开始一条路径，或重置当前的路径
        ctx.moveTo(0, 0);
        ctx.lineTo(500, 290);
        ctx.stroke(); // 在画布上绘制确切的路径
    </script>
</body>

</html>


-----------------------------------

<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <script src="http://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>
    <style media="screen">
        canvas {
            border: 1px solid grey;
            width: 500px; /* canvas 的渲染宽度 */
            height: 300px;
        }
    </style>
</head>

<body>
    <canvas id="canvas">Your browser does not support canvas.</canvas>
    <button type="button" name="button">Canvas 内容</button>
    <img src="">

    <script>
        var canvas = $('#canvas').get(0);
        canvas.width = 500; // canvas 的实际宽度，默认是 300
        canvas.height = 300;
        var ctx = canvas.getContext('2d');

        ctx.fillStyle = '#FFF';
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        ctx.save();

        ctx.translate(100, 100);
        ctx.beginPath();
        ctx.moveTo(0, 0);
        ctx.lineTo(200, 20);
        ctx.lineTo(100, 150);
        ctx.closePath();

        ctx.lineWidth = 4;
        ctx.lineJoin = 'round';
        ctx.fillStyle = '#FFDD11';
        ctx.strokeStyle = 'darkred';
        ctx.fill();
        ctx.stroke();

        ctx.restore();

        ctx.fillStyle = 'rgba(200, 10, 233, 0.4)'; // pink
        ctx.fillRect(0, 0, 200, 200);
        ctx.clearRect(10, 10, 20, 20);

        // 绘制文本
        ctx.save()
        ctx.translate(10, 50);
        ctx.font = '微软雅黑';
        ctx.textAlign = 'left';
        ctx.fillStyle = 'black';
        ctx.fillText('道格拉斯狗', 0, 0);
        ctx.restore();

        // 画园圆弧
        ctx.save()
        ctx.translate(200, 0);
        ctx.beginPath(); // 不加这一句会从上一个 path 画一条线到圆心
        ctx.arc(100, 100, 50, 0, Math.PI * 2, true);
        ctx.fill();
        ctx.stroke();
        ctx.restore();

        // 画图
        var img = new Image();
        img.onload = function() {
            ctx.imageSmoothingEnabled = true;
            ctx.drawImage(img, 0, 150, 128, 128);
        };
        // img.src = 'avatar.jpg'; // 加载图片

        // 获取 canvas 的内容
        $('button').click(function(event) {
            // 当有 canvas 中绘制了图片，如果和 canvas 不是同源的，则 toDataURL() 报安全错误
            $('img').attr('src', canvas.toDataURL()); // Base64 格式
            // console.log(canvas.toDataURL('image/png'));
        });

    </script>
</body>

</html>

```



