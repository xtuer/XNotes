## 下载 Youku 视频

* [http://www.downfi.com/video/](http://www.downfi.com/video/)，需要使用 Chrome，下载的视频为多个分段的视频
* 使用 you-get 下载 [https://github.com/soimort/you-get](https://github.com/soimort/you-get)，下载后会合并为一个视频文件

  * brew install you-get

  * 获取视频信息: `you-get -i 'videoPageUrl'`:

    > \# download-with: you-get --format=mp4 \[URL\]
    >
    > videoPageUrl 需要使用单引号括起来，不能使用双引号

  * 下载视频: `you-get --format=mp4 'videoPageUrl'`

    > m3u8\_url 的 URL 可以在浏览器里直接观看视频

## Mac Grapher

曲线公式为 y = condition ? expression，condition 部分限制 x, y 的作用域，可以设置曲线的颜色，线宽等:![](/assets/normal/grapher.png)

