###### //Daehyeon Kim   
###### //Final Project - Programming Concepts   
###### //CS099   
###### //Spring, 2020   
The Search of Mother   
=============
### Topics   
1. Shapes   
Tiles will make with `square`or`rect`.   
ex) `square(x, y, this.resolution - 1)`   
Baby dinosaur and his googly eyes and various obstacles will make with `arc`, `ellipse`, `vertex`, `bezierVertex`.   
ex) `ellipse(a, b, 20, 30)`   
These are essence of create visual elements.
2. Colors   
Main theme of color will be green. But, I'll express darkness of night via color alpha   
ex)   
```
let a = dinoX - portalX   
let b = dinoY - portalY   
let dis = sqrt(a*a+b*b)   
let c = 0   
color(0,c)   
map(c,400,0,0,220)
```
The color can improve the quality of the game, and in this game, it can also control the difficulty.   
3. Variables   
There is many `const`.   
First, Phase   
ex)   
```
Main menu = 0   
Play = 1   
Setting = 2   
```
Second, Set basic condition   
```
Dead = 0   
Live = 1    
```
Also, there is many 'var' and 'let'   
First, Various Position.   
```
var x = 0   
vay y = 0   
```
Second, Find Distance   
-> same example with color   
These make it easy to set cases.   
4. Conditional Statements   
This will mainly use for check when dinosaur must died.   
```
if(dinoY <350 && dinoX > 50 || dinoY > 50 && dinoX > 50...)   
{dinoStatus = Dead}   
```
And it will use for check button clicked.   
```
if(buttonClicked) {   
...   
}   
```
And it will use for setting when night will come.   
```
if(stage == 3) {   
  push()   
  color(0,c)   
  rect(0,0,width,height)   
  pop()   
} else if (stage >= 4) {   
  push()   
  color(0,220)   
  rect(0,0,width,height)   
  pop()   
}   
```   
By sharing the quarter, you can set the results in detail in a given situation.   
5. Loops   
Mainly use for express terrain - tile based(Grid).   
```
mapCreate(a, b, pattern) {
    let h = obj[pattern].length
    let w = obj[pattern][0].length
    for (let x = 0; x < w + a; x++) {
      for (let y = 0; y < h + b; y++) {
        this.grid[(x + this.cols) % this.cols][(y + this.rows) % this.rows] = obj[pattern][y][x]
      }
    }
  }
```   
Use to perform a certain action repeatedly. It can prevent hard coding.
6. Functions   
Mainly use for read to key is pressed   
```
function keyPressed {   
if(keyCode == 65)   
a += 0.5   
if(keyCode == 68)   
a -= 0.5 -->this is for roll Googly eyes   
```   
While useful for many situations, p5.js' unique functions can be coded more comfortably if they are used in the right place.
7. Classes   
Mainly use for express terrain - tile based.   
And use for make various obstacles   
```
class grid{   
...   
}   
```    
Various factors that are similar but have large populations can be simply written in `Draw`.   
8. Arrays   
Mainly use for express terrain - tile based.   
And use for make random obstacles.   
```
var mapTile[   
[   
  [0,1,0,0,0,1],   
  [0,1,0,1,0,1],   
  [0,1,0,1,0,1],   
  [0,0,0,1,0,0],   
]   
]   
```
Non-regular variables can be organized and used at once, and in the case of creating this game, the terrain can be easily expressed.
