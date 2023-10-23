# ZeehansPortfolio
Hi, I am Zeehan and this is my portfolio


[ShootTheColourCode.txt](https://github.com/ZeehanAbdunNafi/ZeehansPortfolio/files/13068505/ShootTheColourCode.txt)
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
    <canvas id="gameCanvas" width="1300" height="610"></canvas>
    <script>
      /* canvasContext.fillStyle='yellow';
canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
splitup
              if(c==mainBlock.thisCol){
               canvasContext.fillStyle=sameColumn[rowCount];
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
              rowCount=rowCount+1;
              }
              else{
                canvasContext.fillStyle=npcBlock[count];
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
              count=count+1;
               }
               */
              /* .
              .
              .
              .
              .
            for(let r=0;r<4;r++){
            for (let c=0;c<4;c++){
              canvasContext.fillStyle='white';
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
             if (r==mainBlock.thisRow && c==mainBlock.thisCol){
              canvasContext.fillStyle=blockColor;
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
             } else if(c==mainBlock.thisCol && !(r==mainBlock.thisRow)){
              canvasContext.fillStyle=sameColumn[rowCount];
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
              rowCount=rowCount+1;
             }
             else if(!(c==mainBlock.thisCol) && !(r==mainBlock.thisRow)){
              canvasContext.fillStyle=fakeList[count];
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
              count=count+1;
             }
            }
           }
              */

        var ballX=1310;
        var canvas;
        var canvasContext;
        var mainBlock=blockNumGen();
        var blockColor=newColorGen();
        var sniperY=400;
        var sniperX=0;
        var sameColumn=[];
        var aimY;
        var aimX;
        var dead=false;
        var score=0;
        for(let i=0;i<3;i++){
            sameColumn.push("");
        }
        var fakeColour=[];
        for(let i=0;i<12;i++){
            fakeColour.push("");
        }
        window.onload=function(){
         canvas=document.getElementById("gameCanvas");
         canvasContext=canvas.getContext("2d");
        setInterval(superSet,50);
        //sniper
        canvas.addEventListener('mousemove',function(evt){
             var mousePos=calcMousePos(evt);
             sniperY=mousePos.y;
             sniperX=(mousePos.x)-30;
        })
        //aim
        canvas.addEventListener('click',function(evt){
           var mousePos1=calcMousePos(evt);
             aimY=mousePos1.y;
             aimX=mousePos1.x;
             clickRegister();
        })
        }
         function moveBuilding(){
          ballX=ballX-speed();
         }

            //speed
            function speed(){
             if(score<3){
               return 4;
             }
             else if(score<7){
              return 8;
             }
             else if(score<12){
              return 12;
             } else if(score<19){
              return 14;
             }
             else if(score<26){
                 return 18;
             }
             else if(score<40){
                 return 20;
             }
             else if(score<50){
                 return 22;
             } 
             else if(score<70){
                 return 25;
             } else if(score<100){
              return 27;
             }
             else if(score<120){
                 return 28;
             }
             else if(score<145){
                 return 29;
             }
             else if(score<175){
                 return 30;
             }
             else if(score<200){
                 return 32;
             }
             else {
                 return 35;
             }
            }

        function drawBuilding(){
          //while(dead==false){
          canvasContext.fillStyle='black';
         canvasContext.fillRect(0,0,canvas.width,canvas.height);
          canvasContext.fillStyle='silver';
         canvasContext.fillRect(ballX,0,410,610);
         canvasContext.font='bold 50pt Fantasy';
           canvasContext.fillStyle='white';
           if (score<4){
            canvasContext.font='bold 25pt Fantasy';
            canvasContext.fillText("Shoot the target colour at given column.",30,70,800);
            canvasContext.fillText("Do not shoot the edges and the wrong colour.",30,100,800);
            canvasContext.fillText("Shoot before you lose the target color.",30,130,800);
        }
           canvasContext.font='bold 50pt Fantasy'
           canvasContext.fillText(score,0,450,200);
           canvasContext.fillText(blockColor,0,200,200);
           canvasContext.fillText("column",0,305,150);
           canvasContext.fillText(mainBlock.thisCol+1,165,305,50);
           let count=0;
           let colCount=0;
           let colorList=["red","green","blue","yellow"]
           let thisVal=0;
           for(let r=0;r<4;r++){
            for (let c=0;c<4;c++){
              canvasContext.fillStyle='white';
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
             if (r==mainBlock.thisRow && c==mainBlock.thisCol){
              canvasContext.fillStyle=blockColor;
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
             } else if(c==mainBlock.thisCol && !(r==mainBlock.thisRow)){
              while((sameColumn[colCount]=="")||(sameColumn[colCount]==blockColor)){
                thisVal=Math.floor(Math.random()*4);
                sameColumn[colCount]=colorList[thisVal];
              }
              canvasContext.fillStyle=sameColumn[colCount];
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
              colCount=colCount+1;
             }
             else{
              if(fakeColour[count]==""){
              thisVal=Math.floor(Math.random()*4);
              fakeColour[count]=colorList[thisVal];
              }
              canvasContext.fillStyle=fakeColour[count];
              canvasContext.fillRect(ballX+10+(100*c),10+150*r,90,140);
              count=count+1;
             }
            }
  
           }
           
           count=0;
           colCount=0;
          if (ballX+410<0){
              dead=true;
           }
           if(dead==true){
              canvasContext.fillStyle="white";
              canvasContext.fillText("Game over. Refresh to play again.",(canvas.width)/2,200,600)
           }
         canvasContext.fillStyle='pink';
         canvasContext.fillRect(sniperX,sniperY,60,5);
         canvasContext.fillRect(sniperX+30,sniperY-30,5,60);
          }


        function superSet(){
          moveBuilding();
          drawBuilding();
         }
        function newColorGen(){
        let colorList=["red","green","blue","yellow"]
        let thisVal= Math.floor(Math.random()*4);
        return colorList[thisVal];
        }
        function blockNumGen(){
          let row= Math.floor(Math.random()*4);
          let column= Math.floor(Math.random()*4);
          return{
            thisRow: row,
            thisCol: column
        };
      
        }

        function calcMousePos(evt){
        var rect= canvas.getBoundingClientRect();
        var root=document.documentElement;
        var mouseX=evt.clientX-rect.left-root.scrollLeft;
        var mouseY=evt.clientY-rect.top-root.scrollTop;
        return{
            x: mouseX,
            y: mouseY
        };
    }
      function clickRegister(){
        if((aimX>=ballX)&&(aimX<=ballX+410)&&(dead==false)){
           if((aimX>=ballX+10+100*(mainBlock.thisCol))&&(aimX<=ballX+100+100*(mainBlock.thisCol))&&(aimY>=10+150*(mainBlock.thisRow))&&(aimY<=150*(mainBlock.thisRow)+150)){
            ballX=canvas.width;
            mainBlock=blockNumGen();
            blockColor=newColorGen();
            sameColumn=[];
            fakeColour=[];
            score=score+1;
            for(let i=0;i<12;i++){
            fakeColour[i]="";
        }
        for(let i=0;i<3;i++){
            sameColumn[i]="";
        }
           }
           else{
            dead=true;
           }
          }
      }
   

     /*ballX=canvas.width;
            mainBlock=blockNumGen();
            blockColor=newColorGen();
            sameColumn=[];
            fakeColour=[];
            for(let i=0;i<12;i++){
            fakeColour[i]="";
        }
        for(let i=0;i<3;i++){
            sameColumn[i]="";
        }
        aimX=-500;
        aimY=-500;*/
         
       

    </script>
</body>
</html>
