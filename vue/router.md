```html
<button @click="goHome()">Go Home</button>

export default {
    methods: {
        goHome() {
            this.$router.push('/'); // 访问主页
        }
    }
};
```



