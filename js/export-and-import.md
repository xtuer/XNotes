一个模块就是一个独立的文件，该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用 export 关键字输出该变量。

Import 命令输入的变量都是只读的，因为它的本质是输入接口，也就是说，不允许在加载模块的脚本里面，改写接口。如果导入的是一个对象，改写它的属性是允许的。

## Export

```js
<script>
    // foo can be variable or function
    // [1] 定义时导出
    export var foo = 'bar';

    // [2] 先定义，文件最后面再导出
    var foo = 'bar';
    export { foo };

    // [3] 导出可以使用别名
    export { foo as fooz };

    // [4] 导出默认模块: 一个模块只能有一个默认输出
    export default new Vue({});
</script>
```

## Import

```js
<script>
    // [1] 一个一个的导入
    import { foo } from './profile.js';
    import { bar } from './profile.js';

    // [2] 一次导入多个
    import { foo, bar } from './profile.js';

    // [3] 一次导入所有的
    import * from './profile.js';

    // [4] 导入默认模块
    import Vue from './profile.js';

    // [5] 导入可以使用别名
    import { bar as baz } from './profile.js';
</script>
```



