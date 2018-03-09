```html
<template>
    <div>
        <!-- 点击眼睛的 icon 切换密码是否可见 -->
        <Input :icon="type=='password' ? 'eye-disabled' : 'eye'" :type="type" @on-click="changeType"></Input>

        <!-- 和上面的效果一样 -->
        <Input :icon="`eye${type=='password' ? '-disabled' : ''}`" :type="type" @on-click="changeType"></Input>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                type: 'password'
            };
        },
        methods: {
            changeType() {
                if (this.type === 'password') {
                    this.type = 'text';
                } else {
                    this.type = 'password';
                }
            }
        }
    };
</script>
```

![](/assets/normal/iview-password-1.png)

![](/assets/normal/iview-password-2.png)

