---
title: "Second order cone programming"
layout: single
sidebar:
  nav: "tutorials"
---

Let us continue with our regression problem from the linear and quadratic programming tutorials.

The problem boiled down to solving the problem minimize \\(||Ax - y||\\) for some suitable norm. Let us select the 2-norm, but this time solve the extension where we minimize the worst-case cost, under the assumption that the matrix A is uncertain,\\(A=A+d\\), where \\(||d||_2 \leq 1\\). This can be shown to be equivalent to minimizing \\(||Ax-y||_2 + ||x||_2\\).

This problem can easily be solved using YALMIP. Begin by defining the data.

````matlab
x = [1 2 3 4 5 6]';
t = (0:0.02:2*pi)';
A = [sin(t) sin(2*t) sin(3*t) sin(4*t) sin(5*t) sin(6*t)];
e = (-4+8*rand(length(A),1));
y = A*x+e;
````

As a first approach, we will do the modelling by hand, by adding second-order cones using the low-level command [cone](/yalmip/comands/cone).

````matlab
xhat = sdpvar(6,1);
sdpvar u v

F = [cone(y-A*xhat,u), cone(xhat,v)];
solvesdp(F,u + v);
````

By using the automatic modelling support in the [nonlinear operator framework](/yalmip/tutorials/nonlinearoperator), we can alternatively write

````matlab
solvesdp([],norm(y-A*xhat,2) + norm(xhat,2));
````

YALMIP will automatically model this as a second order cone problem, and solve it as such if a [second-order cone programming solver](/yalmip/solvers) is installed. If no second order cone programming solver is found, YALMIP will convert the model to a semidefinite program and solve it using any installed [semidefinite programming solver](/yalmip/solvers)