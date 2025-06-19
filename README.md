# arc.lib
A Singular library for generalized jet schemes computations with fast partial reduction

This is the initial version: arc v1.0.0.0 
and is designed as a supplement to a submitted paper. Later versions are expected. 

This library is basically one main singular procedure arc(ideal, ideal ,ideal , list) where the first ideal is a list of variable of a polynomial ring, the second is a list of generators of an ideal, and the third is a list of generators of a second ideal describing a embedded fat point. The final argument is a list of indexes which sets particular variables to zero. A list of examples will be added later to the folder examles. 

There is a debug version with the debug folder: debugarc v1.0.0.0 which is essentially the same but produces an additional arc_debug.txt file for further development purpose.

Additionally, an alternative version may be later released which uses multinomial long division instead of string hacking. 

The additional tools folder will contain some procedures or libraries which the author believes are useful in this context. 