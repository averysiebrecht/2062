


<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="UTF-8">

    <title>2062</title>
    <style>
    #myCanvas {
        background: #FFC0CB;
        border-style: solid;
    }

    #score {
        font-size: 150%;
    }
    </style>


</head>

<body translate="no">
    <div>Avery's Bot Game ~ Score: <span id="score">0</span></div>
    <canvas id="myCanvas" width="600" height="400">
        Your browser does not support canvas
    </canvas>
    <script src='https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js'></script>
    <script id="rendered-js">
    console.clear();

    let bots = [];

    var c = document.getElementById("myCanvas");
    var ctx = c.getContext("2d");

    function makeBot(x, y, r) {
        if(!x){
            x = Math.floor(Math.random() * canvas.width);
        }
        var bot = {};
        bot.x = x;
        bot.y = y;
        bot.r = r;
        bot.dx = 1;
        bot.dy = -.1;
        bot.color = "indigo";
        bot.theta = Math.atan2(bot.dy, bot.dx);
        return bot;
    }


    var myBot = makeBot(20, 30, 15);
    bots.push(myBot);
    myBot.color = "mediumvioletred";
    bots.push(makeBot(100,200,20));
    bots.push(makeBot(40,60,25));
    console.log(bots);


    function drawBot(bot) {
        ctx.beginPath();
        ctx.arc(bot.x, bot.y, bot.r, 0 * Math.PI, 2 * Math.PI);
        ctx.stroke();
        ctx.fillStyle = bot.color;
        ctx.fill();
        ctx.moveTo(bot.x, bot.y);
        ctx.lineTo(bot.x + bot.r * Math.cos(bot.theta), bot.y + bot.r * Math.sin(bot.theta));
        ctx.stroke();
        
    }


    function moveBot(bot) {
        bot.x = bot.x + bot.dx;
        bot.y = bot.y + bot.dy;

        if (bot.y - bot.r < 0) {
            bot.dy = -bot.dy;
            if(bot.y - bot.r < 0){
                bot.y = bot.r;
            }
            addOne();
        }

        if (bot.x - bot.r < 0) {
            bot.dx = -bot.dx;
            addOne();
        }

        if (bot.x + bot.r >= c.width) {
            bot.dx = -bot.dx;
            addOne();
        }

        if (bot.y + bot.r >= c.height) {
            bot.dy = -bot.dy;
            addOne();
        }

        bot.theta = Math.atan2(bot.dy, bot.dx);
        drawBot(bot);
    }

    function addOne() {
        var score = $("#score").text();
        $("#score").text(Number(score) + 1)
    }

    function moveBots(){
        ctx.clearRect(0, 0, c.width, c.height);
        // moveBot(bots[0]);
        // moveBot(bots[1]);
        for(i = 0; i< bots.length; i++){
            moveBot(bots[i]);
        }
    }
    setInterval(moveBots, 10, myBot);
    

    $("body").keydown(onKeyDown);

    function onKeyDown(e) {
        console.log(e.key);
        e.preventDefault();

        if(e.key=="w"){
            myBot.y = myBot.y - 5;
        }

        if (e.key == " ") {
            console.log("hi Gary");
            myBot.dy= 0;
            myBot.dx = 0;
        }
        if (e.key == "ArrowUp") {
            myBot.dy = myBot.dy - 1;
        }
        if (e.key == "ArrowDown") {
            myBot.dy = myBot.dy + 1;
        }
        if (e.key == "ArrowLeft") {
            myBot.dx = myBot.dx - 1;
        }

    }
    </script>
</body>

</html>
