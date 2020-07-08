###### //Daehyeon Kim   
###### //Final Project - Programming Concepts   
###### //CS099   
###### //Spring, 2020   
The Search of Mother   
=============
### Topics   
1. Shapes    
thorn is made with `line`
```
push()
translate(this.wallPosiX + this.size / 2, this.wallPosiY + this.size / 2)
for (let a = 0; a <= PI; a += PI / 16) {
  rotate(a)
  line(-20, 0, 15, 0)
}
for (let a = PI / 8; a <= PI; a += PI / 4) {
  push()
  rotate(a)
  stroke(2)
  line(-25, 0, 25, 0)
  pop()
}
pop()
```
Baby dinosaur and his googly eyes and various obstacles will make with `circle`, `ellipse`, `vertex`, `bezierVertex`.   
```
draw_Dino() {
    push()
    translate(this.x, this.y)
    rotate(this.angle)
    push()
    fill(this.color)
    ellipse(0, 0, this.dinosize, this.dinosize + 20)
    pop()
    circle(-7.5, -15, 15)
    circle(7.5, -15, 15)
    push()
    fill(0)
    translate(cos(this.r.Get()) * 4.5, sin(this.r.Get()) * 4.5)
    circle(-8, -15, 5)
    circle(8, -15, 5)
    pop()
    pop()
}
draw_Ptero() {
    push()
    translate(this.x, this.y)
    rotate(this.angle)
    fill(this.color)
    beginShape()
    vertex(0, -20)
    vertex(5, -7)
    vertex(4, -2)
    bezierVertex(7, -2, 10, -4, 25, -2)
    bezierVertex(25, -2, 5, 10, 4, 38)
    bezierVertex(4, 38, 4, 17, 0, 15)
    bezierVertex(0, 15, -4, 17, -4, 38)
    vertex(-4, 38)
    bezierVertex(-4, 38, -5, 10, -25, -2)
    bezierVertex(-25, -2, -10, -4, -4, -2)
    vertex(-5, -7)
    endShape(CLOSE)
    push()
    fill(255)
    circle(-3, -10, 6)
    circle(3, -10, 6)
    pop()
    push(0)
    fill(0)
    translate(cos(this.r.Get()) * 1.5, sin(this.r.Get()) * 1.5)
    circle(-3, -10, 2)
    circle(3, -10, 2)
    pop()
    pop()
  }
 ```
These are essence of create visual elements.
2. Colors   
Main theme of color will be green. But, I'll express darkness of night via color alpha    
```
    ...
    push()
    noStroke()
    fill(0, nightWillCome()-110)
    rotate(this.roll)
    arc(0, 0, 3000, 3000, this.roll + PI / 5, this.roll + 9 * PI / 5)
    pop()
    ...
    
function nightWillCome() {
  let dist
  if (stage == 1) {
    return 0
  } else if (stage == 2) {
    dist = getDist(BabyDino, tile1.cx, tile1.cy)
    return map(dist * dist * dist * dist, 547000000000, 0, 0, 255)
  } else if (stage >= 3) {
    return 255
  }
}
```
The color can improve the quality of the game, and in this game, it can also control the difficulty.   
3. Variables   
There is many `const`.   
Phase    
```
const MAINMENU = 1
const SETTING = 2
const HTP = 3
const CREDITS = 4
const PLAY = 5
const CLEAR = 6
const PAUSE = 7
const SETTING2 = 8
const YOUDIED = 9  
```
Also, there is many 'let'   
First, Switch
```
let screamSwitch = false
let crySwitch = false
let dieSoundSwitch = false
let runningSwitch = false
```
Second, For noise  
```
let noiseP1
let noiseP2  
const frame1 = 500
const frame2 = 5000

function draw() {
...
  noiseP1 = float(count % frame1) / frame1
  noiseP2 = float(count % frame2) / frame2
  count++
...
}
```
These make it easy to set cases.   
4. Conditional Statements   
This will mainly use for what happen when baby dinosaur move to something 
```
 if(stage <= 4) {
 if (dino.x >= this.wallPosiX - d && dino.y >= this.wallPosiY && dino.x <= this.wallPosiX + this.size && dino.y <= this.wallPosiY + this.size) {
   dino.x = this.wallPosiX - d
 } else if (dino.x >= this.wallPosiX && dino.y >= this.wallPosiY && dino.x <= this.wallPosiX + this.size + d && dino.y <= this.wallPosiY + this.size) {
   dino.x = this.wallPosiX + this.size + d
 } else if (dino.x >= this.wallPosiX && dino.y >= this.wallPosiY - d && dino.x <= this.wallPosiX + this.size && dino.y <= this.wallPosiY + this.size) {
   dino.y = this.wallPosiY - d
 } else if (dino.x >= this.wallPosiX && dino.y >= this.wallPosiY && dino.x <= this.wallPosiX + this.size && dino.y <= this.wallPosiY + this.size + d) {
   dino.y = this.wallPosiY + this.size + d
 }
 } else if (stage == 5) {
   if (dino.x >= this.wallPosiX - 5*d && dino.y >= this.wallPosiY && dino.x <= this.wallPosiX + this.size && dino.y <= this.wallPosiY + this.size) {
   currentScene = YOUDIED
 } else if (dino.x >= this.wallPosiX && dino.y >= this.wallPosiY && dino.x <= this.wallPosiX + this.size + 5*d && dino.y <= this.wallPosiY + this.size) {
   currentScene = YOUDIED
 } else if (dino.x >= this.wallPosiX && dino.y >= this.wallPosiY - 5*d && dino.x <= this.wallPosiX + this.size && dino.y <= this.wallPosiY + this.size) {
   currentScene = YOUDIED
 } else if (dino.x >= this.wallPosiX && dino.y >= this.wallPosiY && dino.x <= this.wallPosiX + this.size && dino.y <= this.wallPosiY + this.size + 5*d) {
   currentScene = YOUDIED
 }
 }
```
And it will use for check button clicked.   
```
update() {
    if (this.play.DidClickButton()) {
      currentScene = PLAY
      bgs.stop()
      gamebgs.loop()
    } else if (this.setting.DidClickButton()) {
      currentScene = SETTING
    } else if (this.HowtoPlay.DidClickButton()) {
      currentScene = HTP
    } else if (this.credits.DidClickButton()) {
      currentScene = CREDITS
    }
  }  
```
And it will use for setting when night will come.   
```
function nightWillCome() {
  let dist
  if (stage == 1) {
    return 0
  } else if (stage == 2) {
    dist = getDist(BabyDino, tile1.cx, tile1.cy)
    return map(dist * dist * dist * dist, 547000000000, 0, 0, 255)
  } else if (stage >= 3) {
    return 255
  }
}
```   
By sharing the quarter, you can set the results in detail in a given situation.   
5. Loops   
Mainly use for express terrain - tile based(Grid).   
```
Create() {
    this.grid = this.make2DArray(this.cols, this.rows);
    let h = mapMaker[this.pattern].length
    let w = mapMaker[this.pattern][0].length
    for (let x = 0; x < w; x++) {
      for (let y = 0; y < h; y++) {
        this.grid[x][y] = mapMaker[this.pattern][y][x]
        if (mapMaker[this.pattern][y][x] == 1) {
          if (stage !== 5) {
            mapMaker[this.pattern][y][x] = floor(random(2)) + 2
          } else if (stage == 5) {
            mapMaker[this.pattern][y][x] = 4
          }
        }
      }
    }
  }
```   
Use to perform a certain action repeatedly. It can prevent hard coding.
6. Functions   
Mainly use for read to key is pressed   
```
function keyPressed() {
  if (keyCode == 82 && currentScene == PLAY && !textboxSwitch) {
    BabyDino.x = 25
    BabyDino.y = 25
    BabyDino.angle = 0
    BabyDino.roll = PI / 4
  } else if (keyCode == 27) {
    if (currentScene == PLAY) {
      currentScene = PAUSE
    } else if (currentScene == YOUDIED) {
      currentScene = PLAY
      switch (stage) {
        case 1:
          BabyDino.x = 25
          BabyDino.y = 25
          break;
        case 2:
          BabyDino.x = 775
          BabyDino.y = 25
          break;
        case 3:
          BabyDino.x = 175
          BabyDino.y = 25
          CallObstacle.stage3_Dino.stage3_Dino1.x = 775
          runningSwitch = false
          CallObstacle.stage3_Dino.velocity_stage3_x1 = 0
          break;
        case 4:
          BabyDino.x = 525
          BabyDino.y = 375
          break;
        case 5:
          BabyDino.x = 75
          BabyDino.y = 25
          break;
      }
      diebgs.stop()
      if (stage !== 4) {
        gamebgs.loop()
      } else if (stage == 4) {
        hunterbgs.loop()
      }
      dieSoundSwitch = false
    }
  } else if (keyCode == 65 && currentScene == PLAY && !textboxSwitch) {
    BabyDino.roll += PI / 16
  } else if (keyCode == 68 && currentScene == PLAY && !textboxSwitch) {
    BabyDino.roll -= PI / 16
  }
}
```   
While useful for many situations, p5.js' unique functions can be coded more comfortably if they are used in the right place.
7. Classes   
Mainly use for express terrain - tile based.   
And use for make various obstacles   
```
class object {
  constructor(posiX, posiY, col1, col2, col3, ang) {
    this.x = posiX
    this.y = posiY
    this.color = [col1, col2, col3]
    this.angle = ang
  }

}

class obstacle extends object {
...
}

class babydino extends object {
...
}
```    
Various factors that are similar but have large populations can be simply written in `Draw`.   
8. Arrays   
Mainly use for express terrain - tile based.   
And use for make random obstacles.   
```
var mapMaker = [
  [
    [0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0],
    [0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0],
    [0, 1, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1, 1, 1, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0],
    [1, 0, 1, 1, 0, 1, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0],
    [0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0, 1],
    [1, 1, 0, 0, 0, 1, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1],
    [0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 1, 0, 0, 0],
    [0, 1, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0],
    [0, 0, 0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 1],
    [0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0]
  ],
  [
    [0, 1, 1, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0],
    [0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0],
    [0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0],
    [0, 0, 0, 1, 1, 1, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0],
    [0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 0],
    [1, 1, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 1],
    [0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 1, 0],
    [0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 1, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0],
    [0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1, 0, 1, 0],
    [0, 0, 0, 1, 0, 1, 0, 1, 1, 1, 0, 0, 0, 0, 0, 0]
  ],
  [
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 0],
    [0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0],
    [0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0],
    [0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0],
    [0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0],
    [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
  ],
  [
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 0],
    [0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0],
    [0, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 0, 1, 1, 0, 1, 0, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 1, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0],
    [0, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0],
    [0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0],
    [0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0],
    [0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
  ],
  [
    [1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1],
    [0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 1, 1, 1, 0, 0],
    [0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0],
    [0, 1, 0, 1, 1, 1, 1, 0, 1, 1, 0, 1, 0, 1, 0, 0],
    [0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0],
    [0, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0],
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0],
    [1, 1, 0, 1, 0, 1, 1, 0, 1, 1, 1, 1, 1, 0, 1, 0],
    [0, 1, 0, 1, 0, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0],
    [0, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 1, 1, 0, 0],
    [1, 1, 0, 1, 1, 1, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0],
    [0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0]
  ]
]  
```
Non-regular variables can be organized and used at once, and in the case of creating this game, the terrain can be easily expressed.
