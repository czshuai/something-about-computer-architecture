Branch predictors that use the behavior of other branches to make a prediction are called ***correlating predictors*** or ***two-level predictors***.
   
In the general case, an (m,n) predictor uses the behavior of the last m branches to choose from 2^m branch predictors, each of which is an n-bit predictor for a single branch.
   
***Tournament predictors*** take this insight to the next level, by using multiple predictors, usually one based on global information and one based on local information, and combining them with a selector.