+++
date = '2024-12-23T18:23:08+08:00'
draft = false
title = 'Line fitting'
math = true
+++

# What is line fitting?

This is actually one derived case of optimization problem; linear optimization to be more precise. As we need to be able to tell or model a tendency out of a bunch of samples that may look irregular at first, we need certain mathematical tools to do so. In all these mathematical tools, we recurr to optimization to help us model a bunch of samples a reasonable model. 

# Why do we do line fitting?

For instance, under the context of determining a straight line out of a randomly but somewhat distributed points in the space, we want to determine whether there is a line formed by these points. This scenario ocurs frequently in finding lines in a 2D images that may be regarded as horizon lines to determine the vanishing point. Or simply to look for lines to serve as edges in the image to help us better determine how much has the camera moved based on how much variations are there in these lines or __features__ as called by computer vision practitioners.

# Problem formulation

So for instance, we have a set of points in the space that somehow has a tendency to form a line or a straight edge in the space. More interesting yet, we have multiple sets of points that exhibit 

## Type 1 fitting:  $min \left\| Ax - b\right\|^2$

A linear model:

$
y = Ax + b
$

We can establish an error term for each sample in the set defined as

$
e = \left| y_i - a x_i - b\right|
$

in which $y_i$ is the dependent variable and $a x_i - b$ serves as the model to be estimated.

Now we can broaden the previous expression to a linear system it looks like the following:

$$
E = \left| \begin{bmatrix}
y_1 \\
\vdots \\
y_n
\end{bmatrix} - 
\begin{bmatrix}
x_1 &  & 1 \\
\vdots &  & \vdots \\
x_n &  & 1 \\
\end{bmatrix}
\begin{bmatrix}
c \\ d
\end{bmatrix}
 \right|^2 
$$

$ E \equiv \left\| b - Ax \right\| $

$ E = \left\| b^2 - 2bAx + \underbrace{(Ax)^2}_{\text{Actually this does not exist}} \right\|^2 $

$ E = \left\| b^2 \right\| - 2b^TAx + x^TA^TAx $

$ E = b^T b - 2b^T Ax + x^T A^T Ax $

Let's minimize the error E we get

$ \frac{\partial E}{\partial x} = -2b^TA + 2A^TAx = 0 $

$ \therefore b^T A = A^T A x $

which in terms we can also look at this expression as

$ \overbrace{A^T Ax}^{ax} = \overbrace{b^T A}^{b} \text{ given }\left\| b \right\| \neq 0  $

## Type 2 fitting: $ min \left\| Ax \right\|^2 $

Give the line model $ ex + fy + g = 0 $:

$ E_i = \left| ex_i + fy_i + g \right| $

$ E_i = \sum_{i = 1}^{N} (ex_i + fy_i + g)^2 $

$$

E_i = \left\| \begin{bmatrix}
x_1 & y_1 & 1 \\
\vdots & \vdots & \vdots \\
x_n & y_n & 1 \\
\end{bmatrix} \right\|^2

$$

$$
E_i = \left\| Ax \right\|^2  \text{subject to } \left\| x \right\| \text{ otherwise we will get trivial solution x = 0}
$$

and if we decompose $ Ax $ with the Singular value decomposition (SVD) appraoch we will get,

$ \left\| USV^T x \right\|^2 $

in which $ V = \begin{bmatrix}
v_1 & v_2 & v_3 \\
\end{bmatrix} $

and $ v_3 $ is the solution we are looking for.

This is not all. If $ rank(A) = n - 1 $ then the linear system has exactly one solution. On the contrary, as $ rank(A) \neq m $ and even $ rank(A) < m $, where $m$ is the number of eigenvectors or variables needed to solve the sytem, then we can conclude that the system is underdetermined.

These two types of fitting approaches are also known as the least square method that we will come back in later articles.


