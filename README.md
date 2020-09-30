<style>
.bg {
  margin:0px;
  padding:0px;
  width: 100vw;
  height:100vh;
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  background: #4a569d;
}
.bgContainer {
  width: 800px;
  height: 400px;
  background: linear-gradient(to bottom, #4a569d, #348ac7);
  position: relative;
  box-shadow: 0 0 5px #333;
  overflow: hidden;
  border-radius: 15px;
}
.bgContainer .tree {
  position: absolute;
  background: #336699;
  clip-path: polygon(50% 0, 0 100%, 100% 100%);
  bottom: 0;
}
.bgContainer .tree:nth-child(1) {
  left: -100px;
  width: 200px;
  height: 400px;
  z-index: 2;
  background:#5387BC
}
.bgContainer .tree:nth-child(2) {
  left: 8px;
  width: 150px;
  height: 300px;
  z-index: 2;
}
.bgContainer .tree:nth-child(3) {
  left: 100px;
  width: 250px;
  height: 350px;
  opacity: 0.7;
  background:#5387BB
}
.bgContainer .tree:nth-child(4) {
  left: 160px;
  width: 300px;
  height: 200px;
  z-index: 3;
  background:#2E6194
}
.bgContainer .tree:nth-child(5) {
  left: 500px;
  width: 100px;
  height: 150px;
  z-index: 2;
  background:#3A6DA5;
}
.bgContainer .tree:nth-child(6) {
  left: 650px;
  width: 300px;
  height: 300px;
  opacity: 0.7;
  z-index: 3;
  background:#556699;
}
.bgContainer .tree:nth-child(7) {
  left: 580px;
  width: 100px;
  height: 200px;
  z-index: 3;
}
.bgContainer .tree:nth-child(8) {
  left: 470px;
  width: 50px;
  height: 50px;
  z-index: 1;
  background:#295C8F;
}
.bgContainer .tree:nth-child(9) {
  left: 380px;
  width: 150px;
  height: 300px;
  opacity: 0.9;
  z-index: 0;
  background:#5387BC;
}
.bgContainer .moon {
  position: absolute;
  width: 80px;
  height: 80px;
  background: #fff;
  right: 20px;
  top: 50px;
  border-radius: 50%;
  box-shadow: 0 0 10px #ddd;
}
.bgContainer .moon:before {
  content: "";
  position: absolute;
  width: 15px;
  height: 15px;
  clip-path: ellipse(50% 40%);
  background: #f4f4f4;
  left: 15px;
  top: 10px;
}
.bgContainer .moon:after {
  content: "";
  position: absolute;
  width: 10px;
  height: 10px;
  clip-path: ellipse(50% 40%);
  background: #f4f4f4;
  left: 15px;
  top: 30px;
}
.bgContainer .star {
  width: 100%;
  height: 150px;
  position: relative;
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
  </div>
</div>