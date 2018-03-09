```js
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
    <title></title>

<script src="jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
    loadImage("http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_01.jpg");
    loadImage("http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_02.jpg");
    loadImage("http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_03.jpg");
    loadImage("http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_04.jpg");
    loadImage("http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_05.jpg");

    function loadImage(imagePath) {
        var img = new Image();
        $(img).load(function() {
            $(".comingSoonImages-slide-wrap").append(this);
        }).error(function() {
            console.log("Image not found: " + imagePath);
        }).attr("src", imagePath);
    }
});
</script>
</head>
<body>
    <div class="comingSoonImages-slide-wrap">
        <!--<img src="http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_01.jpg" >
        <img src="http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_02.jpg" >
        <img src="http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_03.jpg" >
        <img src="http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_04.jpg" >
        <img src="http://img.game.co.uk/merch2014/comingsoon/xbox360/cs_05.jpg" >-->
    </div>
</body>
</html>
```



