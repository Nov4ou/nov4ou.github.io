---
layout: post
title: Draw A Line in OLED
date: '2023-01-20 02:11:40 +0800'
categories: [Computer Graphics]
tags: [Algorithms]
usemathjax: true
---
# Draw a Straight Line in SSD-1306 OLED Screen

## Preface
To draw a line in the screen, you should determine two points at first. If those points happen to lie in the horizontal line or the vertical line, just light up all the pixels in that line. But in most case we have to draw a line with different slope. There are various method to do it. In this blog I will show two common solutions.

First of all, you should be able to ligth up one pixel, that's the most basic prerequisite. You should get the necessary initialization etc. drivers from the hardware manufacturer.

## Method 1
### Algorithm
With two point we can get the slope of the line. Then we can get the equation as well. Consider the 2-dimensional array as a 2D coordinate system. For each `x`, substituting into the equation yields `y`. Draw all the $$(x, y)$$ to get the line.

![image 1](/assets/img/computergraphics/method1p.svg)

For example, when `x = 2`, `y = 4` by default. as `x` increase, for each `x`, we can get `y` from \(y=y_1+m(x-x_1)\). `x = 3`, `y = 4(4.36)`...so on.

By calculate each `x` and `y`, we can draw all the points to get a line. As the below picture:
![image 2](/assets/img/computergraphics/method1.svg)

### Code
```c  
void OLED_DrawLine(uint8_t x1, uint8_t y1, uint8_t x2, uint8_t y2)
{
  uint8_t tx, ty;
  float slope = (float)(y2 - y1) * 1.000 / (float)(x2 - x1);
  for (uint8_t i = 0; x1 + i <= x2; i++) {
    tx = x1 + i;
    ty = y1 +(uint8_t)(slope * (tx - x1) + 0.5);
    OLED_DrawPoint(tx, ty);
  }
}
```
### Notes
This is the simplist way to draw a line. If the slope is too steep, there may be a problem.

Consdier this example: to draw a line which connect `(2,2)` and `(5, 9)`. The result may lead to this:

![image 3](/assets/img/computergraphics/method1bad.svg)

These scattered points can't form a perfect line. The reason is when the slope is too deep, with every x increase, y decreases much more. To solve this problem, just switch x and y-axis, compute the line as the method above.

## Method 2
This is Bresenham's line algorithm.

![image 4](/assets/img/computergraphics/method2P.svg)

Suppose the endpoints of the line are at $(x_1,y_1)$ and $(x_2, y_2)$.For the sake of presentation, $(x_2-x_1) > (y_2-y_1)$ so the line goes down and to the right. In this octant, for each $x$ between $x_1$ and $x_2$, there is exactly only one row $y$ containing a pixel of the line, while each row between $y_1$ and $y_2$ may contain multiple $x$. 

Bresenham's algorithm chooses the ideal $y$ for each $x$: As $x$ increase, $y$ can remain the same or increase by 1. To decide whether to increase or decrease, a new variable `D` is defined. If $(x_2-x_1) < (y_2-y_1)$, on the contrary, As $y$ increase, $x$ can remain the same or increase by 1. Just switch x and y-axis.

### Derivation
#### Line equation
To derive Bresenham's line algorithm, there are two steps:
- Transform the equation of a line from the slope-intercept form into a function of `x` and `y`;
- Use the new equation to draw a line based on the idea of accumulation of error.

The slope-intercept form of a line
\begin{equation}
y=f(x)=mx+b
\end{equation}
can't represent a vertical line. Therefore, we can transform it to a function of $x$ and $y$ to draw lines at any angle.


\begin{equation}
\begin{aligned}
y &= mx+b \newline 
y &= \frac{\Delta y}{\Delta x}x+b \newline 
(\Delta x)y &= (\Delta y)x+(\Delta x)b \newline 
0 &= (\Delta y)x-(\Delta x)y+(\Delta x)b
\end{aligned}
\end{equation}
<!-- $$(x,y)\Omicron \require{mediawiki-texvc} Ax+By+C=0$$ -->
The last euation can be written as
\begin{equation}
f(x,y):=Ax+By+C=0
\end{equation}
where $$A=\Delta y=y_2-y_1,B=-\Delta x=-(x_2-x_1),C=(\Delta x)b=x_2y_1-x1y_2$$.

This form only involves integers because `x` and `y` are integers, so do `A`,`B`,`C`.

In this example, the equation $y=\frac{2}{5}x+\frac{3}{5}$ can be written as $f(x,y)=-2x+5y-3$. The two endpoints are on the line:
\begin{equation}
\begin{aligned}
f(1,1)&=-2(1)+5(1)-3=0 \newline
f(11,5)&=-2(11)+5(5)-3=0
\end{aligned}
\end{equation}
and
\begin{equation}
\begin{aligned}
f(3,4)&=-2(3)+5(4)-3=11>0 \newline
f(11,2)&=-2(11)+5(2)-3=-15<0
\end{aligned}
\end{equation}
![image 5](/assets/img/computergraphics/method2plane.svg)

The line splits x-y plane into halves. The blue one is negative half-plane and the yellow one is positive half-plane.

#### Alogrithm
Start with $(x_0, y_0)$: $f(1, 1)=0$ and $(1,1)$ lies on the line. Now the next move is to decide whether the next pixel is $(x_0+1, y_0)$ or $(x_0+1, y_0+1)$. The chosen one should be closer to the line. Evaluate the line function at the midpoint:
\begin{equation}
f(x_0+1, y_0+\frac{1}{2})
\end{equation}
![image 6](/assets/img/computergraphics/methodalo.svg)
