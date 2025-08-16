# arc.lib
A Singular library for generalized jet schemes computations with fast partial reduction

This is the initial version: arc v2.0.0.0 
and is designed as a supplement to a submitted paper. Later versions are expected. 

This library is basically one main singular procedure arc(ideal, ideal ,ideal , list) where the first ideal is a list of variables of a polynomial ring, the second is a list of generators of an ideal, and the third is a list of generators of a second ideal describing a embedded fat point. The final argument is a list of indexes which sets particular variables to zero. A list of examples will be added later to the folder examples. 

There is a debug version with the debug folder: debugarc v1.0.0.0 which is essentially the same but produces output files arc_original_output.txt, arc_output.txt, and arc_debug.txt file for further development purposes. 

Examples: 
 //Example 1:
  ring R = 0, (x,y), dp;
  ideal Vars = x,y;
  ideal I = x^4 + y^3;
  ideal J = x^2,y^2;       // fat point at origin
  list L;                 //  optional skips
  def s = arc(Vars, I, J, L);
  setring s;
  ideal A = arcideal;
  A;
==> A[1]=a1^4+a2^3
==> A[2]=4*a1^3*a3+3*a2^2*a4
==> A[3]=4*a1^3*a5+3*a2^2*a6
==> A[4]=12*a1^2*a3*a5+4*a1^3*a7+6*a2*a4*a6+3*a2^2*a8
 //Example 2: 
  ring R = 0, (x,y), dp;
  ideal Vars = x,y;
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
 //Example 3:
ring R = 0 ,(x,y), dp;
ideal V = x,y;
ideal I = xy; 
ideal K = x3; 
def s = arc(V, I, K, list());
setring s;
ideal A = arcideal;
A;
==> A[1]=a1*a2
==> A[2]=a2*a3+a1*a4
==> A[3]=a3*a4+a2*a5+a1*a6
 //Example 4: 
ring R = 0, (x(1..4)), dp;
ideal V = x(1), x(2), x(3), x(4);
ideal I = x(1)**2 - 2*x(2)*x(3) + x(1)*x(4)**2;
ideal J = x(4)^5;
def s = arc(V, I, J, list());
setring s;
ideal A = arcideal;
A;
==> A[1]=a1*a4^2+a1^2-2*a2*a3
==> A[2]=a4^2*a5+2*a1*a4*a8+2*a1*a5-2*a3*a6-2*a2*a7
==> A[3]=2*a4*a5*a8+a1*a8^2+a4^2*a9+2*a1*a4*a12+a5^2-2*a6*a7+2*a1*a9-2*a3*a10-2*a2*a11
==> A[4]=a5*a8^2+2*a4*a8*a9+2*a4*a5*a12+2*a1*a8*a12+a4^2*a13+2*a1*a4*a16+2*a5*a9-2*a7*a10-2*a6*a11+2*a1*a13-2*a3*a14-2*a2*a15
==> A[5]=a8^2*a9+2*a5*a8*a12+2*a4*a9*a12+a1*a12^2+2*a4*a8*a13+2*a4*a5*a16+2*a1*a8*a16+a4^2*a17+2*a1*a4*a20+a9^2-2*a10*a11+2*a5*a13-2*a7*a14-2*a6*a15+2*a1*a17-2*a3*a18-2*a2*a19
 //Example 4:
ring R = 0, (x,y), dp;
ideal V = x,y;
ideal I = y2- x3, x4, x3y;
list L;
def s = arc(V,I,I,L);
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
 //Example 5:
ring R = 0, (x,y), dp;
ideal V = x,y;
ideal I = y2- x3, x4, x3y;
list L=1,2,4;
def s = arc(V,I,I,L);
setring s;
ideal A = arcideal;
A;
==> A[1]=-3*a3^2*a7+2*a6*a8
==> A[2]=-a3^3+a8^2
