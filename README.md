<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./css.css">
    <style>
    </style>
</head>
<body>
    <!-- 中奖与不中奖的音乐 -->
    <audio src="./audio/y1209.mp3" id ="y1209"></audio>
    <audio src="./audio/y1037.mp3" id ="y1037"></audio>
    <!-- 最外层的盒子 -->
    <div class="container">
        <!-- 8个小灯 -->
        <div class="box1 size"></div>
        <div class="box2 size"></div>
        <div class="box3 size"></div>
        <div class="box4 size"></div>
        <div class="box5 size"></div>
        <div class="box6 size"></div>
        <div class="box7 size"></div>
        <div class="box8 size"></div>
        <!-- 转盘设置 -->
        <img src="./images/turntable.png">
        <div class="top"><img src="./images/top.png" alt="" ></div>
        <div class="pointer" id="pointer"><img src="./images/pointer.png" alt=""></div>

        <!-- 显示抽奖情况的 -->
        <div class="text" id="decoration"></div>      
    </div>
    <!-- 抽奖按钮 -->
    <input type="button" value="幸运转转" id="button">
    
    <script>
        // 随机生成角度，同时使用户无法抽到一等奖
        let rotateNum=Math.floor(Math.random()*360)+1;
        while(rotateNum>180 && rotateNum<225){
            rotateNum=Math.floor(Math.random()*360)+1;
            if(!(rotateNum>180 && rotateNum<225)){
            break;
            }
        }
        let rotateNum2 = rotateNum;
        // 随机生成圈数
        let rotateTimes=Math.floor(Math.random()*10)+3;
        rotateNum=rotateTimes*360+rotateNum;        
        // 按钮点击时转动，并且设置每6秒才能触发一次
        let time = 0;
        document.getElementById('button').onclick = function(){
            if(time == 0){
                time =6;
                let index = setInterval(function(){
                    time--;
                    if(time == 0){
                        clearInterval(index);

                    }
                },1000);
                document.getElementById('pointer').style.transform =  'rotate('+rotateNum+'deg)';
            }else{
                console.log("目前按钮不可用")
            }
        
            // 判断角度，显示抽奖情况
            setTimeout(function(){
                let i=6;
                document.getElementById('decoration').style.opacity=1;
                setInterval(function(){
                    if(rotateNum2>0 && rotateNum2<45){
                        document.getElementById("decoration").innerHTML="恭喜您,获得三等奖！倒计时<span id='time'>"+i+"</span>秒后重新开始";
                        let au = document.getElementById('y1037');
                        au.play();
                    }else if (rotateNum2>90 && rotateNum2 < 135){
                        document.getElementById("decoration").innerHTML="恭喜您,获得四等奖！倒计时<span id='time'>"+i+"</span>秒后重新开始";
                        let au = document.getElementById('y1037');
                        au.play();
                    }else if(rotateNum2>270 && rotateNum2<315){
                        document.getElementById("decoration").innerHTML="恭喜您,获得二等奖！倒计时<span id='time'>"+i+"</span>秒后重新开始";  
                        let au = document.getElementById('y1037');
                        au.play();
                    }else{
                        document.getElementById("decoration").innerHTML="别沮丧！再来一次吧！倒计时<span id='time'>"+i+"</span>秒后重新开始";
                        let au2 = document.getElementById('y1209');
                        au2.play();
                    }
                        i--;
                    if (i ==0){
                        window.location.reload()
                    }
                },1000)
           
            },6000);
        }
    </script>
</body>
</html>
