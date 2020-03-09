---
title: “Datastructures”
description: “ This chapter introduces the organization of data creative designers organize information.”
authors:  ['rajaa_issa']
languages: unset
platforms: ['Windows', 'Mac']
categories: ['Essential Mathematics']
origin: ""
order: "65"
tags: ['mathematics', 'geometry', 'grasshopper3d']
---
*Transformations* refer to operations such as moving (also called *translating*), rotating, and scaling objects. They are stored in 3 D programming using matrices, which are nothing but rectangular arrays of numbers. Multiple transformations can be performed very quickly using matrices. It turns out that a [4x4] matrix can represent all transformations. Having a unified matrix dimension for all transformations saves calculation time.

<!-- $$\begin{array}{rcc} \mbox{matrix}&\begin{array}{cccc} c1& c2&c3&c4\end{array}\\\begin{array}{c}row(1)\\row(2)\\row(3)\\row(4)\end{array}& \left[\begin{array}{cr} +&+&+&+\\  +&+&+&+\\ +&+&+&+\\ +&+&+&+\end{array}\right] \end{array}$$ -->

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

$$\mathbf{V}_1 \times \mathbf{V}_2 =
   \begin{vmatrix}
    \mathbf{i} & \mathbf{j} & \mathbf{k} \newline
    \frac{\partial X}{\partial u} & \frac{\partial Y}{\partial u} & 0 \newline
    \frac{\partial X}{\partial v} & \frac{\partial Y}{\partial v} & 0 \newline
   \end{vmatrix}$$

## 2.1 Matrix operations

The one operation that is most relevant in computer graphics is matrix multiplication. We will explain it with some detail.

### Matrix multiplication

Matrix multiplication is used to apply transformations to geometry. For example if we have a point and would like to rotate it around some axis, we use a rotation matrix and multiply it by the point to get the new rotated location.


<div>$$\begin{array}{ccc} \text{rotate matrix} & \text{input point}  & \text{rotate point}\\\begin{bmatrix}a & b & c & d \\e & f & g & h \\i & j & k & l \\0 & 0 & 0 & 1 \\\end{bmatrix}& \cdot\begin{bmatrix}x \\y\\z\\1 \\\end{bmatrix}&= \begin{bmatrix}x' \\y'\\z'\\1 \\\end{bmatrix}\end{array}$$</div>    

Most of the time, we need to perform multiple transformations on the same geometry. For example, if we need to move and rotate a thousand points, we can use either of the following methods.

**Method 1**  

1. Multiply the move matrix by 1000 points to move the points.
2. Multiply the rotate matrix by the resulting 1000 points to rotate the moved points.  

Number of operations = **2000**.  

**Method 2**  

1. Multiply the rotate and move matrices to create a combined transformation matrix.
2. Multiply the combined matrix by 1000 points to move and rotate in one step.

Number of operations = **1001**.

Notice that method 1 takes almost twice the number of operations to achieve the same result. While method 2 is very efficient, it is only possible if both the move and rotate matrices are $[4 \times 4]$. This is why in computer graphics a $[4 \times 4]$ matrix is used to represent all transformations, and a $[4 \times 1]$ matrix is used to represent points.

Three-dimensional modeling applications provide tools to apply transformations and multiply matrices, but if you are curious about how to mathematically multiply matrices, we will explain a simple example. In order to multiply two matrices, they have to have matching dimensions. That means the number of columns in the first matrix must equal the number of rows of the second matrix. The resulting matrix has a size equal to the number of rows from the first matrix and the number of columns from the second matrix. For example, if we have two matrices, $M$ and $P$, with dimensions equal to $[4\times 4]$ and $[4 \times 1]$ respectively, then there resulting multiplication matrix $M · P$ has a dimension equal to $[4 \times 1]$ as shown in the following illustration:

$$\begin{array}{ccc} M & P  & P' \\\begin{bmatrix}\color{red}{a} & \color{red}{b}  & \color{red}{c} & \color{red}{d}  \\e & f & g & h \\i & j & k & l \\0 & 0 & 0 & 1 \\\end{bmatrix}& \cdot\begin{bmatrix}\color{red}{x} \\\color{red}{y} \\\color{red}{z} \\\color{red}{1}  \\\end{bmatrix}&= \begin{bmatrix}\color{red}{x'=a*x+b*y+c*z+d*1}\\y'=e*x+f*y+g*z+h*1\\z'=i*x+j*y+k*z+l*1 \\1=0*x+0*y+0*z+1*1\\\end{bmatrix}\end{array}$$  
