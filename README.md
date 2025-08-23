# arc.lib
A Singular library for generalized jet schemes computations with fast partial reduction.

## Description:
This library is basically one main singular procedure def S = arc(ideal ,ideal , list). The first two arguments (which are ideals) occur in a basring R (this basering should be of characteristic zero). The first ideal is the ideal of definition of an affine scheme X, and the second describes a embedded fat point in X. To be clear, an embedded fat point is given by an ideal J  such that the auxiliary ring D created by only the variables used in J creates a zero dimensional quotient ring D/J. The third argument is a list of indexes which sets particular variables to zero. A list of examples will be added to the folder examples. 



## Notes:
1) In regards to the second argument J, the variables used are usually chosen to be sequential--the first m variables or the last m variables. However, theoretically, any choice of variables from the basering R can be used as long as they define a ring D/J of Krull dimension 0. See previous paragraph fo clarity. 

2) In regards to the third argument, if the user wishes not to set any of the variables to zero, one should input an empty list, which is usually done by running def S = arc(I,J,list()).

3) There is a debug version with the debug folder: debugarc v1.0.0 which is paired down version, but it produces output files arc_original_output.txt, arc_output.txt, and arc_debug.txt file for further development purposes. It can also be useful for exploratory purposes.  



## Goal:
The goal of this project is to provide a library which completes efficient computations of generalized jet schemes of affine algebraic varieties within the Singular computer algebra system. This library represents a significant improvement over previous Sage implementations, offering enhanced speed, reduced memory usage, and a novel iterative reduction approach for studying jet schemes. The software enables direct computation of jet scheme equations with respect to arbitrary fat points, supporting advanced research in singularity theory and algebraic geometry. The lond term goal is to investigate various questions related to partially reduced structures on generalized jet schemes of fat points and related questions raised by the author on induced flatness between reduced generalized jet schemes.



## Examples: 
```
// Example 1:
ring R = 0, (x,y), dp;
ideal I = x^4 + y^3;
ideal J = x^2,y^2;   // fat point at origin
list L = list(1,2);  // fiber of origin
def s = arc(Vars, I, J, L);
setring s;
ideal A = arcideal;
s;
A;
==> // coefficients: QQ considered as a field
==> // number of vars : 6
==> //        block   1 : ordering dp
==> //                  : names    a3 a4 a5 a6 a7 a8
==> //        block   2 : ordering C
==> A[1]=0
```

```
// Example 2: 
ring R = 0, (x,y), dp;
ideal I = x^4 + y^3;
ideal J = x^2,y^2;   // fat point at origin
list L = list(1,2);  // fiber of origin
def s = arc(Vars, I, J, L);
setring s;
ideal A = arcideal;
s;
A;
==> // coefficients: QQ considered as a field
==> // number of vars : 6
==> //        block   1 : ordering dp
==> //                  : names    a3 a4 a5 a6 a7 a8
==> //        block   2 : ordering C
==> A[1]=0
```

```
// Example 3:
ring R = 0 ,(x,y), dp;
ideal I = xy; 
ideal K = x3; 
def s = arc(I, K, list());
setring s;
ideal A = arcideal;
A;
==> A[1]=a1*a2
==> A[2]=a2*a3+a1*a4
==> A[3]=a3*a4+a2*a5+a1*a6
```

 ```
// Example 4: 
ring R = 0, (x(1..4)), dp;
ideal I = x(1)**2 - 2*x(2)*x(3) + x(1)*x(4)**2;
ideal J = x(4)^5;
def s = arc(I, J, list());
setring s;
ideal A = arcideal;
A;
==> A[1]=a1*a4^2+a1^2-2*a2*a3
==> A[2]=a4^2*a5+2*a1*a4*a8+2*a1*a5-2*a3*a6-2*a2*a7
==> A[3]=2*a4*a5*a8+a1*a8^2+a4^2*a9+2*a1*a4*a12+a5^2-2*a6*a7+2*a1*a9-2*a3*a10-2*a2*a11
==> A[4]=a5*a8^2+2*a4*a8*a9+2*a4*a5*a12+2*a1*a8*a12+a4^2*a13+2*a1*a4*a16+2*a5*a9-2*a7*a10-2*a6*a11+2*a1*a13-2*a3*a14-2*a2*a15
==> A[5]=a8^2*a9+2*a5*a8*a12+2*a4*a9*a12+a1*a12^2+2*a4*a8*a13+2*a4*a5*a16+2*a1*a8*a16+a4^2*a17+2*a1*a4*a20+a9^2-2*a10*a11+2*a5*a13-2*a7*a14-2*a6*a15+2*a1*a17-2*a3*a18-2*a2*a19
```

```
// Example 4:
ring R = 0, (x,y), dp;
ideal I = y2- x3, x4, x3y;
list L;
def s = arc(I,I,L);
setring s;
ideal A = arcideal;
A;
==> A[1]=a1^3*a2
==> A[2]=3*a1^2*a2*a3+a1^3*a4
==> A[3]=3*a1*a2*a3^2+3*a1^2*a3*a4+3*a1^2*a2*a5+a1^3*a6
==> A[4]=3*a1^2*a2*a7+a1^3*a8
==> A[5]=6*a1*a2*a3*a7+3*a1^2*a4*a7+3*a1^2*a3*a8+3*a1^2*a2*a9+a1^3*a10
==> A[6]=3*a2*a3^2*a7+6*a1*a3*a4*a7+6*a1*a2*a5*a7+3*a1^2*a6*a7+3*a1*a3^2*a8+3*a1^2*a5*a8+6*a1*a2*a3*a9+3*a1^2*a4*a9+3*a1^2*a3*a10+3*a1^2*a2*a11+a1^3*a12
==> A[7]=a2*a3^3+3*a1*a3^2*a4+6*a1*a2*a3*a5+3*a1^2*a4*a5+3*a1^2*a3*a6+3*a1*a2*a7^2+3*a1^2*a7*a8+3*a1^2*a2*a13+a1^3*a14
==> A[8]=a1^4
==> A[9]=4*a1^3*a3
==> A[10]=6*a1^2*a3^2+4*a1^3*a5
==> A[11]=4*a1^3*a7
==> A[12]=12*a1^2*a3*a7+4*a1^3*a9
==> A[13]=12*a1*a3^2*a7+12*a1^2*a5*a7+12*a1^2*a3*a9+4*a1^3*a11
==> A[14]=4*a1*a3^3+12*a1^2*a3*a5+6*a1^2*a7^2+4*a1^3*a13
==> A[15]=-a1^3+a2^2
==> A[16]=-3*a1^2*a3+2*a2*a4
==> A[17]=-3*a1*a3^2-3*a1^2*a5+a4^2+2*a2*a6
==> A[18]=-3*a1^2*a7+2*a2*a8
==> A[19]=-6*a1*a3*a7-3*a1^2*a9+2*a4*a8+2*a2*a10
==> A[20]=-3*a3^2*a7-6*a1*a5*a7-6*a1*a3*a9-3*a1^2*a11+2*a6*a8+2*a4*a10+2*a2*a12
==> A[21]=-a3^3-6*a1*a3*a5-3*a1*a7^2-3*a1^2*a13+2*a4*a6+a8^2+2*a2*a14
```

```
// Example 5:
ring R = 0, (x,y), dp;
ideal I = y2- x3, x4, x3y;
list L=1,2,4;
def s = arc(I,I,L);
setring s;
ideal A = arcideal;
A;
==> A[1]=-3*a3^2*a7+2*a6*a8
==> A[2]=-a3^3+a8^2
```