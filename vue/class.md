```html
<body>
    <!-- 1 -->
    <div v-bind:class="{ active: true }"></div> ===>
    <div class="active"></div>

    <!-- 2 -->
    <div :class="['active', 'text-danger']"></div> ===>
    <div class="active text-danger"></div>

    <!-- 3 -->
    <div v-bind:class="[{ active: true }, errorClass]"></div> ===>
    <div class="active text-danger"></div>

    --- style ---
    <!-- 1 -->
    <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
    <!-- 2 将多个 样式对象 应用到一个元素上-->
    <div v-bind:style="[baseStyles, overridingStyles]"></div>

    --- script ---
    <script>
        // 2 创建 Vue 的实例对象
        var vm = new Vue({
            el: '#app',
            data: {
                activeColor: 'red',
                fontSize: 30,

                baseStyles: {
                    color: 'red',
                    'font-size': '30px'
                },
                overridingStyles: {
                    color: 'green',
                }
            }
        })
    </script>
</body>
```

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>测试</title>
    <script src="http://cdn.jsdelivr.net/npm/vue"></script>
    <style media="screen">
        body {
            font-family: "微软雅黑", Helvetica, Arial, sans-serif;
        }

        .active {
            background: red;
        }
        .focus {
            border: 1px dashed blue;
            padding: 2px;
        }
    </style>
</head>

<body>
    <!-- Vue 使用的模版 -->
    <div id="vue-app">
        <span v-text="msg" v-bind:class="{active: active, focus: active}"></span>
        <button @click="changeClass">Change Class(生效)</button>
    </div>

    <script>
        var app = new Vue({
            el: '#vue-app',
            data: {
                msg: 'Hello',
                active: true
            },
            methods: {
                changeClass() {
                    this.active = !this.active;
                }
            }
        });
    </script>
</body>

</html>
```



