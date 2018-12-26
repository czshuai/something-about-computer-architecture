The key idea behind implementing speculation is to allow instructions to ***execute out of order*** but to force them to ***commit in order*** and to prevent any irrevocable action (such as updating state or taking an exception) until an instruction commits. 
   
We call the additional step in the instruction execution sequence ***instruction commit***.
   
The hardware buffer, which we call the ***reorder buffer*** (ROB), is also used to pass results among instructions that may be speculated.

There are the four steps involved in instruction execution:
 1. Issue.
 2. Execute.
 3. Write result.
 4. Commit.

