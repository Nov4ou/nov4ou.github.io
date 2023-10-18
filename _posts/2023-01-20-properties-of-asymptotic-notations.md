---
layout: post
title: Properties of Asymptotic Notations
date: '2023-01-20 02:46:55 +0800'
categories: [Introduction to algorithm 3th]
tags: [Algorithms]
---
# Asymptotic Notations:
<!-- >   $$ -->
$ \Theta(g(n))=\left\\{ f(n): there \ exist \ positive \ constants \ c_1, \ c_2, \ and \ n_0 \ such \ that 0 \leq c_1g(n) \leq f(n) \leq c_2g(n) \ for \ all \ n \geq n_0 \right\\}. $
$ O(g(n))=\left\\{ f(n): there \ exist \ positive \ constants \ c \ and \ n_0
\right. \left.\ such \ that \ 0 \leq f(n) \leq cg(n) \ for \ all \ n \geq n_0 \right\\}. $
$ \Omega(g(n))=\left\\{ f(n): there \ exist \ positive \ constants \ c \ and \ n_0
\right. \left.\ such \ that \ 0 \leq cg(n) \leq f(n) \ for \ all \ n \geq n_0 \right\\}. $
$ o(g(n))=\left\\{ f(n): for \ any \ positive \ constant \ c>0, \ there \ exist
\right. \left.\ a \ constant \ n_0>0 \ such \ that \ 0 \leq f(n) < cg(n) \ for \ all \ n \geq n_0 \right\\}. $
$ \omega(g(n))=\left\\{ f(n): for \ any \ positive \ constant \ c>0, \ there \ exist
\right. \left.\ a \ constant \ n_0>0 \ such \ that \ 0 \leq cg(n) < f(n) \ for \ all \ n \geq n_0 \right\\}. $

# Properties:
**Reflexivity:**
If $f(n)$ is given then
\begin{equation}
f(n) = O(f(n))
\end{equation}
*Example:* 
If $f(n)=n^3 \Rightarrow O(n^3)$
Similarly,
\begin{equation}
f(n) = Ω(f(n))
\end{equation}
\begin{equation}
f(n) = Θ(f(n)) 
\end{equation}
        
**Symmetry:**
\begin{equation}
f(n) = \Theta(g(n)) \ if \ and \ only \ if \ g(n)=\Theta(f(n)) 
\end{equation}
*Example:*
If $f(n)=n^2$ and $g(n)=n^2$ then $f(n)=\Theta(n^2)$ and $g(n)=\Theta(n^2)$

***Proof:***
-   ***Necessary part:*** 
\begin{equation}
f(n) = \Theta(g(n)) \Rightarrow g(n) = \Theta(f(n))
\end{equation}
By the definition of $\Theta$, there exists positive constants $c_1$, $c_2$ and $n_0$ such that
\begin{equation}
0 \leq c_1g(n) \leq f(n) \leq c_2g(n)
\end{equation}
for all $n \geq n_0$ 
$\Rightarrow
g(n) \leq (\frac{1}{c_1}) \cdot f(n) \ and \ g(n) \geq (\frac{1}{c_2}) \cdot f(n)
$
$
\Rightarrow
(\frac{1}{c_2}) \cdot f(n) \leq g(n) \leq (\frac{1}{c_1}) \cdot f(n)
$
Since $c_1$ and $c_2$ are positive constants, $\frac{1}{c_1}$ and $\frac{1}{c_2}$ are well defined. Therefore, by the definitionof $\Theta$, $g(n)=\Theta(f(n))$
-   ***Sufficiency part:***
\begin{equation}
g(n)=\Theta(f(n)) \Rightarrow f(n) = \Theta(g(n))
\end{equation}
By the definition of $\Theta$, there exists positive constants $c_1$, $c_2$ and $n_0$ such that
\begin{equation}
0 \leq c_1f(n) \leq g(n) \leq c_2f(n)
\end{equation}
for all $n \geq n_0$
$
\Rightarrow
f(n) \leq (\frac{1}{c_1}) \cdot g(n) \ and \ f(n) \geq (\frac{1}{c_2}0 \cdot g(n)
$
$
\Rightarrow
(\frac{1}{c_2}) \cdot g(n) \leq f(n) \leq (\frac{1}{c_1}) \cdot g(n)
$
By the definition of $\Theta$, $f(n)=\Theta(g(n))$

**Transistivity:**
\begin{equation}
f(n)=O(g(n)) \ and \ g(n)=O(h(n)) \Rightarrow f(n)=O(H(n))
\end{equation}
*Example:*
If $f(n)=n$, $g(n)=n^2$ and $h(n)=n^3$
$\Rightarrow$ $n$ is $O(n^2)$ and $n^2$ is $O(n^3)$ then $n$ is $O(n^3)$

***Proof:***
\begin{equation}
f(n)=O(g(n)) \ and \ g(n) = O(h(n)) \Rightarrow f(n)=O(h(n))
\end{equation}

By the definition of $O$, there exists positive constants $c$, $n_0$ such that $f(n) \leq cg(n)$ for all $n \geq n_0$
$
\Rightarrow
f(n) \leq c_1g(n)
$
$
\Rightarrow
g(n) \leq c_2h(n)
$
$
\Rightarrow
f(n) \leq c_1c_2h(n)
$
$
\Rightarrow
f(n) \leq ch(n), where, c = c_1 \cdot c_2.
$
By the definition, $f(n) = O(h(n))$
Similarly,
\begin{equation}
f(n)=\Theta(g(n)) \ and \ g(n) = \Theta(h(n)) \Rightarrow f(n)=\Theta(h(n))
\end{equation}
\begin{equation}
f(n)=\Omega(g(n)) \ and \ g(n) = \Omega(h(n)) \Rightarrow f(n)=\Omega(h(n))
\end{equation}
\begin{equation}
f(n)=o(g(n)) \ and \ g(n) = o(h(n)) \Rightarrow f(n)=o(h(n))
\end{equation}
\begin{equation}
f(n)=\omega(g(n)) \ and \ g(n) = \omega(h(n)) \Rightarrow f(n)=\omega(h(n))
\end{equation}

**Transpose Symmetry:**
\begin{equation}
f(n)=O(g(n)) \ if \ and \ only \ if \ g(n)=\Omega(f(n)) 
\end{equation}
*Example:*
if $f(n)=n$ and $g(n) = n^2$ then $n$ is $O(n^2)$ and $n^2$ is $\Omega(n)$

***Proof:***
-   ***Necessary part:***
\begin{equation}
f(n) = O(g(n)) \Rightarrow g(n) = \Omega(f(n))
\end{equation}
By the definition of $O \Rightarrow f(n) \leq cg(n)$ for some positive constant $c \Rightarrow g(n) \geq (\frac{1}{c}) \cdot f(n)$ 

By the definition of $\Omega$, $g(n)=\Omega(f(n))$
-   ***Sufficiency part:***
\begin{equation}
g(n) = \Omega(f(n)) \Rightarrow f(n)=O(g(n))
\end{equation}

By the definition of $\Omega$, for some positive constants $c \Rightarrow g(n) \geq cf(n) \Rightarrow f(n) \leq (\frac{1}{c})\cdot g(n)$

By the definition of O, $f(n) = O(g(n))$

Similarly,
\begin{equation}
f(n)=o(g(n)) \ if \ and \ only \ if \ g(n) = \omega(f(n))
\end{equation}

**Observations:**
\begin{equation}
max(f(n), g(n)) = \Theta(f(n)+g(n))
\end{equation}
***Proof:***
Without loss of generality, assume $f(n) \leq g(n)$ $\Rightarrow max(f(n), g(n)) = g(n)$

Consider $g(n) \leq max(f(n), g(n)) \leq g(n)$
\begin{align} 
& \Rightarrow g(n) \leq max(f(n), g(n)) \leq f(n) + g(n) \newline
& \Rightarrow \frac{g(n)}{2} + \frac{g(n)}{2} \leq max(f(n), g(n)) \leq f(n) + g(n)
\end{align}
From what we assumed, we can write
\begin{equation}\Rightarrow \frac{f(n)}{2}+\frac{g(n)}{2} \leq max(f(n), g(n)) \leq f(n) + g(n)\end{equation}
\begin{equation}\Rightarrow \frac{f(n)+g(n)}{2} \leq max（f(n), g(n)) \leq f(n)+g(n)\end{equation}
By the definition of $\Theta$, $max(f(n), g(n)=\Theta(f(n)+g(n)))$

## O(f(n))+O(g(n))=O(max(f(n), g(n)))
***Proof:***
Without loss of generality, assume $f(n) \leq g(n)$
\\[\Rightarrow
O(f(n)) + O(g(n)) = c_1 \cdot f(n) + c_2 \cdot g(n)\\]
From what we assumed, we can write
\begin{equation}
O(f(n)) + O(g(n)) \leq c_1 \cdot g(n) + c_2 \cdot g(n) \\\\
\leq (c_1+c_2)g(n) \\\\
\leq cg(n) \\\\
\leq c \cdot max(f(n), g(n))
\end{equation}
By the definition of $O$,
\begin{equation}
O(f(n)) + O(g(n)) = O(max(f(n), g(n)))
\end{equation}

# References
1. [properties-of-asymptotic-notations](https://www.geeksforgeeks.org/properties-of-asymptotic-notations/)
2. [Introduction to Algorithms Third Edition](https://mitpress.mit.edu/9780262533058/)