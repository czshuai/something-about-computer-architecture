To obtain the final unrolled code we had to make the following decisions and transformations:
 1. Determine that unrolling the loop would be useful by finding that the loop iterations were independent.
 2. Use different registers to avoid unnecessary constraints that would be forced by using the same registers for different computations.
 3. Eliminate the extra test and branch instructions and adjust the loop termination and iteration code.
 4. Determine that the loads and stores in the unrolled loop can be interchanged by observing that the loads and stores from different iterations are independent.
 5. Schedule the code, preserving any dependences needed to yield the same result as the original code.
   
    
Three different effects limit the gains from loop unrolling:
 - A decrease in the amount of overhead amortized with each unroll.
 - Code size limitations. (instruction cache miss rate)
 - Compiler limitations. (register pressure)