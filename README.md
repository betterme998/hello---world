<!DOCTYPE html>
<html>
    <head>
        <meta charset='utf-8'>
        <meta name="viwport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum.scale=1.0, user-scalable=no">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="Keywords" content="追随鼠标">
        <meta name="description" content="不同颜色小球 跟随鼠标">
        <title>Canvas - mouse moving colorful balls</title>
        <style>
            body{
                display: grid;
                justify-content: center;
                align-content: center;
            }
          canvas {
            border:1px solid #000;
          }
        </style>
    </head>
    <body>
        <canvas id = "mycanvas" width = "1320" height = "600"></canvas>
        <script>
          var mycanvas = document.getElementById('mycanvas');
          var ctx = mycanvas.getContext("2d");
         
          var circleArr = [];
         
          function Circle(x,y,r,color){
            this.x = x;
            this.y = y;
            this.r = r;
            this.color = "rgb(" + (parseInt(Math.random() *240) + 9) + "," + (parseInt(Math.random() *220) + 18) + ", 203)";
            
            this.dx = Math.random() * 12 -7;
            this.dy = Math.random() * 12 - 7;
            
            circleArr.push(this);
          }
          
          //the renderer
          Circle.prototype.rander = function(){
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.r, 0, Math.PI*2, true);
            ctx.fillStyle = this.color;
            ctx.fill();
          }
          
          Circle.prototype.update = function(){
            this.x += this.dx;
            this.y += this.dy;
            this.r--;
            
            if(this.r < 0){
              for(var i = 0; i < circleArr.length; i++){
                if(circleArr[i] === this){
                  circleArr.splice(i,1);
                }
              }
              return false;
            }
            return true;
          }
          
          mycanvas.onmousemove = function(event){
            new Circle(event.clientX, event.clientY, 30, "red");
          }
          
          setInterval(function(){
            ctx.clearRect(0, 0, 1320, 600)
            for (var i = 0; i < circleArr.length; i++){
              circleArr[i].update() && circleArr[i].rander();

            }
          }, 20);
        </script>
    </body>

</html>
