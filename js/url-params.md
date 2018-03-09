```html
<body>
    <video id="myVideo" width="670" height="377" autoplay="true" controls="controls">
        <source src="" type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"'>
    </video>
    <br>
    <a id="myTarget" href="">Target</a>

    <script type="text/javascript">
        // 地址示例
        // http://localhost/x.html?video=http://192.168.10.126/tih.mp4&target=http://www.baidu.com
        // http://edu-edu.com/b2c-static/parter-try.html?video=http://192.168.10.126/tih.mp4&target=http://www.baidu.com
        var url = new URL(window.location.href);        // 当前网页的地址
        var videoUrl  = url.searchParams.get("video");  // 获取地址中的 video 参数
        var targetUrl = url.searchParams.get("target"); // 获取地址中的 target 参数

        document.querySelector("#myVideo > source").src = videoUrl; // 设置视频的地址
        document.querySelector("#myTarget").href = targetUrl;       // 设置跳转链接的地址
    </script>
</body>
```

```js
function getQueryParam(name) {
    var found;
    window.location.search.substr(1).split("&").forEach(function(item) {
        if (name == item.split("=")[0]) {
            found = item.split("=")[1];
        }
    });
    return found;
};
```



