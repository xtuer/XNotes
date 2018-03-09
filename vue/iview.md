### Rate props {#Rate_props}

| Property | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| count | Star count. | Number | 5 |
| value | Current value. Use v-model to enable a two-way binding. | Number | 0 |
| allow-half | Whether to allow semi selection. | Boolean | false |
| disabled | Read only, unable to interact. | Boolean | false |
| show-text | Whether to display a prompt text. | Boolean | false |

iview 中属性，都可以使用 v-bind 或者 : 进行绑定，Boolean 的属性比较特别，为 true 时直接出现即可，可以不用 : 进行绑定，例如下面的 allow-half, show-text 和 count 的使用

```html
<Rate v-model="result" allow-half :show-text="true" :count="6">
    <span style="color: #f5a623">{{ result * 1000 }} 人</span>
</Rate>
```

* **字符串的属性**: 可以不用绑定直接赋值，如 `status="active"`
* **数字的属性**: 不能直接赋值，需要使用 : 进行绑定，如 `:count="6"`，`count="6"` 则报错传入的是字符串，需要一个数字
* **Boolean 的属性**: 
  * 如果出现在 tag 中表示为 true，此时不需要绑定和赋值，如 `allow-half` 
  * `allow-half="false"` 则还是为 true
  * 为 false 时不出现在 tag 中或者使用绑定，如 `:allow-half="false"`



