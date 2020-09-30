### Hi there 👋

<style >
  $borderStyle: 1px solid #ccc;
$bgColor: linear-gradient(to bottom, #4a569d, #348ac7);
$treeColor: #336699;
$disLeft: 800px;
$random: random() * 10 px;
.bg {
  width: 100vw;
  height: 100vh;
  background: #4a569d;
  display: flex;
  justify-content: center;
  align-items: center;
}
.bgContainer {
  width: 800px;
  height: 400px;
  background: $bgColor;
  position: relative;
  box-shadow: 0 0 5px #333;
  overflow: hidden;
  border-radius: 15px;

  .tree {
    position: absolute;
    background: $treeColor;
    clip-path: polygon(50% 0, 0 100%, 100% 100%);
    bottom: 0;

    &:nth-child(1) {
      left: $disLeft/-8;
      width: 200px;
      height: 400px;
      z-index: 2;
    }
    &:nth-child(2) {
      left: $disLeft/100;
      width: 150px;
      height: 300px;
      z-index: 2;
    }
    &:nth-child(3) {
      left: $disLeft/8;
      width: 250px;
      height: 350px;
      background: $treeColor + 5;
      opacity: 0.7;
    }
    &:nth-child(4) {
      left: $disLeft/5;
      width: 300px;
      height: 200px;
      background: $treeColor - 5;
      z-index: 3;
    }
    &:nth-child(5) {
      left: $disLeft - 300;
      width: 100px;
      height: 150px;
      background: $treeColor + 5;
      z-index: 2;
    }
    &:nth-child(6) {
      left: $disLeft - 150;
      width: 300px;
      height: 300px;
      background: $treeColor + 45;
      opacity: 0.7;
      z-index: 3;
    }
    &:nth-child(7) {
      left: $disLeft - 220;
      width: 100px;
      height: 200px;
      background: $treeColor - 10;
      z-index: 3;
    }
    &:nth-child(8) {
      left: $disLeft / 2 + 70;
      width: 50px;
      height: 50px;
      background: $treeColor + 25;
      z-index: 1;
    }
    &:nth-child(9) {
      left: $disLeft / 2 - 20;
      width: 150px;
      height: 300px;
      background: $treeColor + 35;
      opacity: 0.9;
      z-index: 0;
    }
  }
  .moon {
    position: absolute;
    width: 80px;
    height: 80px;
    background: #fff;
    right: 20px;
    top: 50px;
    border-radius: 50%;
    box-shadow: 0 0 10px #ddd;
    &:before {
      content: "";
      position: absolute;
      width: 15px;
      height: 15px;
      clip-path: ellipse(50% 40%);
      background: #f4f4f4;
      left: 15px;
      top: 10px;
    }
    &:after {
      content: "";
      position: absolute;
      width: 10px;
      height: 10px;
      clip-path: ellipse(50% 40%);
      background: #f4f4f4;
      left: 15px;
      top: 30px;
    }
  }
  .star {
    width: 100%;
    height: 150px;
    position: relative;

    &:before {
    }
    &:after {
    }
  }
}

</style>
<div class="bg">
  <div class="bgContainer">
    <div class="tree"></div>
    <div class="tree"></div>
    <div class="tree"></div>
    <div class="tree"></div>    
    <div class="tree"></div>
    <div class="tree"></div>
    <div class="tree"></div>
    <div class="tree"></div>
    <div class="tree"></div>
    <div class="tree"></div>    
    <div class="moon"></div>
    <canvas id="fwhfCanvas"></canvas> 
  </div>
</div>
<script>
          class FwhfStarrySky {
            constructor() {
                this.canvas = '';
                this.context = '';
                this.timer = null;
                this.mountainArr = [];
                this.starArr = [];
                this.meteorArr = [];
                this.width = 800;
                this.height = 400;
                this.init();
            }
            init() {
                this.canvas = document.getElementById('fwhfCanvas');
                this.canvas.width = this.width;
                this.canvas.height = this.height;
                this.canvas.style.display = 'inline-block';
                this.context = this.canvas.getContext('2d');
                var ladder = 0;
                while (ladder < this.height - 200) {
                    for (var i = 0; i < (this.height - ladder) / 100; i++) {
                        this.starArr.push([this.rand(0, this.width), this.rand(ladder, ladder + 20), this.rand(0,
                            10), 0.1]);
                    }
                    ladder += 20;
                }
                this.drawTimer();
            }
            drawSky() {
                this.context.beginPath();
                var skyStyle = this.context.createLinearGradient(0, 0, 0, this.canvas.height);
              skyStyle.addColorStop(0, "#4a569d");  
              skyStyle.addColorStop(1, "#348ac7");
                this.context.fillStyle = skyStyle;
                this.context.fillRect(0, 0, this.width, this.height);
                this.context.closePath();
            }
            darwStar() {
                this.starArr.forEach((v) => {
                    this.context.beginPath();
                    this.context.fillStyle = "rgba(250,250,250," + v[2] / 10 + ")";
                    this.context.arc(v[0], v[1], 1, 0, 5 * Math.PI);
                    this.context.fill();
                    this.context.closePath();
                });
            }
            drawMeteor() {
                var meteorNum = this.rand(-9, 9);
                if (meteorNum == 1) {
                    this.meteorArr.push([this.rand(0, this.width + this.height), 0, this.rand(1, 3)]);
                }
                this.meteorArr.forEach((v) => {
                    this.context.beginPath();
                    this.context.fillStyle = "rgba(255,255,255,1)";
                    if (v[0] > this.width) {
                        this.context.arc(v[0], v[1] + (v[0] - this.width), 1, 0, 2 * Math.PI);
                    } else {
                        this.context.arc(v[0], v[1], 1, 0, 2 * Math.PI);
                    }
                    this.context.fill();
                    if (v[0] > this.width) {
                        var meteorStyle = this.context.createLinearGradient(v[0], v[1], v[0] + v[2] * 20, v[
                            1] + (v[0] - this.width) - v[2] * 20);
                        meteorStyle.addColorStop(0, "rgba(255,255,255,1)");
                        meteorStyle.addColorStop(1, "rgba(255,255,255,0)");
                        this.context.strokeStyle = meteorStyle;
                        this.context.lineTo(v[0], v[1] + (v[0] - this.width));
                        this.context.lineTo(v[0] + v[2] * 20, v[1] + (v[0] - this.width) - v[2] * 20);
                    } else {
                        var meteorStyle = this.context.createLinearGradient(v[0], v[1], v[0] + v[2] * 20, v[
                            1] - v[2] * 20);
                        meteorStyle.addColorStop(0, "rgba(255,255,255,1)");
                        meteorStyle.addColorStop(1, "rgba(255,255,255,0)");
                        this.context.strokeStyle = meteorStyle;
                        this.context.lineTo(v[0], v[1]);
                        this.context.lineTo(v[0] + v[2] * 20, v[1] - v[2] * 20);
                    }
                    this.context.stroke();
                    this.context.closePath();
                })
                this.meteorArr.forEach((v, index) => {
                    v[0] -= v[2];
                    v[1] += v[2];
                    if (v[0] < -20 || v[1] > this.height) {
                        this.meteorArr.splice(index, 1);
                    }
                })
            }
            drawTimer() {
                this.drawSky();
                this.darwStar();           
                this.drawMeteor();
                this.timer = setInterval(() => {
                    this.starArr.forEach((v) => {
                        if (v[2] + v[3] < 0 || v[2] + v[3] > 10) {
                            v[3] *= -1;
                        }
                        v[2] += v[3];
                    });
                    this.drawSky();     // 夜幕
                    this.darwStar();    // 星星
                    this.drawMeteor();  // 流星
                }, 20)
            }
            rand(min, max) {
                var c = max - min + 1;
                return Math.floor(Math.random() * c + min);
            }
        }
        new FwhfStarrySky();

</script>
