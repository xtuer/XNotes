```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
</head>

<body>
    <script type="text/javascript">
        class Shape {
            draw() {
                console.log('Shape::draw()');
            }
        }

        // 类 + 继承
        class Rect extends Shape {
            // this.x = 0; // Error

            // 构造函数 + 默认参数
            constructor(x = 0, y = 0, width = 100, height = 100) {
                super(); // 构造函数中需要调用父类的构造函数
            }
        }

        class Circle extends Shape {
            constructor(cx, cy, radius) {
                super();

                // 成员变量赋值
                this.cx = cx;
                this.cy = cy;
                this.radius = radius;
            }

            // @Override: 重写父类的函数
            draw() {
                console.log('Circle::draw()');
            }

            // 静态函数
            static className() {
                return 'Circle';
            }

            getRadius() {
                return this.radius;
            }
        }

        var rect = new Rect();
        var circle = new Circle(0, 0, 20);
        rect.draw();   // 调用 Shape.draw()，继承
        circle.draw(); // 调用 Circle.draw()，重写

        console.log(circle.getRadius()); // 成员函数调用
        console.log(Circle.className()); // 静态函数调用
    </script>
</body>

</html>

```



