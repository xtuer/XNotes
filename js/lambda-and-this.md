```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>
</head>

<body>
    <script type="text/javascript">
        var bar = 20; // window.bar
        var foo = {
            animate: function() {
                return this; // foo
            },
            swing() { // ES5 class, is equal to swing: function() {}
                return this; // foo
            },
            gumi: () => { // Lambda, is not equal to gumi: function() {}
                return this; // window
            }
        };

        console.log(foo.swing() == foo.animate()); // true
        console.log(foo.swing() == foo.gumi()); // false
    </script>
</body>

</html>
```



