
# turtle库初识

## 绘制蟒蛇


```python
import turtle as t

def drawSnake(rad, angle, len, neckrad):
    for i in range(len):
        t.circle(rad, angle)
        t.circle(-rad, angle)
    t.circle(rad, angle/2)
    t.fd(rad)
    t.circle(neckrad+1, 180)
    t.fd(rad*2/3)


t.setup(1000, 500, 0, 0)
t.up()
t.goto(-400, 0)
t.down()
t.pensize(30)
t.pencolor('blue')
t.seth(-40)
drawSnake(40, 80, 5, 15)
```

![蟒蛇](http://static.zybuluo.com/liangxw/gsq7pi4m980n504z25662eg4/image_1bdgci4l11pkhfdomnd1s6g1e6g13.png)

## 函数解析

- turtle.setup()  
turtle中的turtle.setup()函数用于启动一个图形窗口，它有四个参数`turtle.setup(width, height, startx, starty)`  
分别是：启动窗口的宽度，高度，以及窗口左上角在屏幕中的坐标位置。  
我们所使用的显示屏幕也是一个坐标系，该坐标系以**左上角**为原点，向右和向下分别是x轴和y轴：  
![屏幕坐标系统](http://static.zybuluo.com/liangxw/cumx458dw2fnaxgxeef3tfm7/image_1bdd4030bge1nh81b1d1j7213q9.png)

- turtle.up()和turtle.down()   
turtle.up()为提起画笔  
turtle.down()为放下画笔

- turtle.goto()  
初始时刻，小乌龟在启动窗口的正中央，坐标为(0, 0)（此为画图窗口的原点，而不是屏幕的原点），向右和向上为正方向。  
通过turtle.goto(x, y)可以将小乌龟移动到(x, y)坐标处。

- turtle.pensize()  
turtle.pensize(size)函数表示小乌龟**运动轨迹的宽度**，单位为像素。
- turtle.pencolor()  
turtle.pencolor(color)函数表示小乌龟运动轨迹的**颜色**。  
turtle采用RGB方式来定义颜色，如turtle.pencolor("#3B9909")。

- turtle.seth()  
turtle.seth(angle)函数表示小乌龟**初始时运动方向**。  
输入参数是一个角度值，其中0表示向东，90度向北，180度向西，270度向南；负值表示的方向与正值表示的方向关于方向0对称：  
![angle表示方向](http://static.zybuluo.com/liangxw/u7hcs8d5zncanffjmz5qfa67/image_1bde3j2cd1k0av1qth81lqs63n1g.png)

- turtle.circle()  
turtle.circle(rad, angle)函数让小乌龟沿着一个**圆形**爬行。  
参数rad描述圆形轨迹**圆心**的位置，rad>0时，圆心在当前速度方向的左侧；当rad<0时，圆心在当前速度方向的右侧；  
参数angle表示小乌龟沿着圆形爬行的角度值，angle>0表示逆时针运动，angle<0表示顺时针运动。  
> 如下图所示，此时rad>0，angle<0。
![](http://static.zybuluo.com/liangxw/l1u4axw8apujrcowd961bxx3/image_1bdgbqdij1fkfkt512e03fh2bk9.png)

- turtle.fd()  
turtle.fd(distance)或者turtle.forward()表示乌龟沿当前方向**直线**爬行，爬行距离为distance

## 彩色蟒蛇


```python
import turtle as t

def drawSnake(rad, angle, len, neckrad):
    color = ['red', 'yellow', 'green', 'black', 'blue']
    for i in range(len):
        # 更改画笔颜色
        t.pencolor(color[i])
        t.circle(rad, angle)
        t.circle(-rad, angle)
    t.pencolor('purple')
    t.circle(rad, angle/2)
    t.fd(rad)
    t.circle(neckrad+1, 180)
    t.fd(rad*2/3)


t.setup(1000, 500, 0, 0)
t.up()
t.goto(-400, 0)
t.down()
t.pensize(30)

t.seth(-40)
drawSnake(40, 80, 5, 15)
```

![彩色蟒蛇](http://static.zybuluo.com/liangxw/08toglbs7p9gmwalrrp0bzpn/image_1bdgcfkgaq7u1vmv1o91jlp1rerm.png)

# 常用函数

## 控制画笔绘制状态的函数

```python
pendown() | pd() | down()
penup() | pu() | up()
pensize(wid ) | width(wid)
```

## 控制画笔颜色和字体函数

```python
color()  reset()
begin_fill()  end_fill()
filling()  clear()
screensize()
## 显示或隐藏小乌龟
showturtle() | st()
hideturtle() | ht()
isvisible()
write(arg, move=False, align="left", font =("Arial",8,"normal") )
```

## 控制画笔运动的函数

```python
forward(distance) | fd(distance)
backward(distance)| bk(distance) | back(distance)
## 小乌龟向右侧转动一定的角度
right(angle) | rt(angle)
left(angle) | lt(angle)
setheading(to_angle)
position() | pos()
goto(x,y )
setposition(x,y ) | setpos(x,y )
circle(radius,extent ,steps )
dot(size ,*color) radians()
stamp() speed(speed )
clearstamp(stamp_id)
clearstamps(n ) undo()
speed(speed ) heading()
towards(x,y ) distance(x,y )
xcor() ycor()
setx(x) sety(y)
home() undo()
degrees(fullcircle = 360.0)
```

## TurtleScreen/Screen类的函数

```python
bgcolor(*args)
bgpic(picname)
clearscreen()
resetscreen()
screensize(cwid ,canvh,bg )
tracer(n ,delay )
listen(xdummy ,ydummy )
onkey((fun,key)
onkeyrelease((fun,key)
onkeypress(fun,key )
onscreenclick(fun,btn=1,add)
getcanvas()
getshapes()
turtles()
window_height()
window_width()
bye()
exitonclick()
title(titlestring)
setup(wid = _CFG["wid"], h = _CFG["h"], startx = _CFG["leftright"], starty = _CFG["topbottom"])
```

# 应用举例

## 绘制等边三角形


```python
import turtle as t

t.seth(60)
t.fd(200)
t.seth(-60)
t.fd(200)
t.seth(-180)
t.fd(200)
t.ht()
```

![等边三角形](http://static.zybuluo.com/liangxw/6ma6z5beohy4nllngih0ujll/image_1bdgcooht1gdo1nvvtab9eq1vvg1g.png)

## 绘制红色五角星


```python
from turtle import *

fillcolor("red")
pencolor("red")
begin_fill()
while True:
    forward(200)
    right(144)
    # abs()是求当前位置离原点的距离
    if abs(pos()) < 1:
        break
end_fill()
ht()
```

![五角星](http://static.zybuluo.com/liangxw/d8ofm5oyxxaw4hn8nlrsffjc/image_1bdgeoc4i1r6f1etg1m6g5n1mju1t.png)

## 绘制太阳花


```python
from turtle import *
## 第一个为画笔颜色，第二个为填充颜色
color('red', 'yellow')

begin_fill()
while True:
    forward(200)
    left(170)
    if abs(pos()) < 1:
        break
end_fill()
done()
```

![太阳花](http://static.zybuluo.com/liangxw/papoae4sr19f1xvrpeayzd19/image_1bdgetuki1r3n180tgfi1bg9k022a.png)

## 绘制螺旋线


```python
import turtle

turtle.speed("fastest")
turtle.pensize(2)
## 左侧
turtle.up()
turtle.goto(-100, 0)
turtle.down()
for x in range(100):
    turtle.forward(2 * x)
    turtle.left(90)
## 右侧
turtle.up()
turtle.goto(100, 0)
turtle.down()  
turtle.seth(90)
for x in range(20):
    turtle.circle(5 * x, 180)
```

![螺旋线](http://static.zybuluo.com/liangxw/45d33fuhv0wq65ks8kh95wzi/image_1bdgfh2ftjiu123ia7p1lk7qdk2n.png)
    


## 彩色螺旋线


```python
import turtle
import time
turtle.pensize(2)
turtle.bgcolor("black")
colors = ["red", "yellow", 'purple', 'blue']
## 延迟更新图纸，可用于加速绘制复杂图形
turtle.tracer(False)
for x in range(400):
    turtle.forward(2*x)
    turtle.color(colors[x % 4])
    turtle.left(91)
turtle.tracer(True)
```

![彩色螺旋线](http://static.zybuluo.com/liangxw/3rl7nq4mlhnztjz11ymm40m8/image_1bdgfvonh1qbe1r0krptcn5rt34.png)
