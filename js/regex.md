```js
/**
 * URL 的模式是 /admin/topics/1234/questions
 * 可以使用正则从 URL 中取得 topic id.
 *
 * @return topic's id
 */
Question.getTopicId = function() {
    var topicId = 0; // 默认值
    var href = window.location.href;
    var regex = /admin\/topics\/(\d+)\/questions/;

    href.replace(regex, function() {
        topicId = arguments[1];
    });

    return topicId;
}
```



