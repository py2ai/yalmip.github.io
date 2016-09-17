---
title: "CUTSDP"
layout: single
permalink: /solvers/cutsdp/
sidebar:
  nav: "solvers"
---

Built-in mixed-integer solver for convex conic problems.

### YALMIP
CUTSDP is invoked with `sdpsettings('solver','cutsdp')@@`

### Comments

CUTSDP is a simple solver for mixed-integer second-order cone and semidefinite programs, implementing a cutting plane (outer approximation) approach. In contrast to [BNB] which relaxes the integer variables in the problem and proceeds by branch-and-bound, solving conic programs problem in every node, CUTSDP relaxes the conic constraints to linear constraints, solves a mixed-integer linear program, and adds violating linear cuts to the model and repeats.

CUTSDP is an internal experimental implementation with little testing performed, although it has been successfully applied on some real-world problems.

The solver relies on fast external mixed integer linear programming solvers.