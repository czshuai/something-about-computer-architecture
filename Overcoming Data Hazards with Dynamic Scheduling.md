Dynamic scheduling -- Rearranges the instruction execution to reduce the stalls while maintaining data flow and exeception behavior.
   
Dynamic scheduling offers several advantages:
- It allows code that was compiled with one pipeline in mind to run efficiently on a different pipeline, eliminating the need to have multiple binaries and recompile for a different microarchitecture.
- It enables handling some cases when dependences are unknown at compile time.
- It allows the processor to tolerate unpredictable delays.

   
We separate the issue process into two parts: checking for any structural hazards and waiting for the absence of a data hazard. Thus, we still use in-order instruction issue, but we want an instruction to begin execution as soon as its data operands are available. Such a pipeline does ***out-of-order exection***

   
Split the ID pipe stage of our simple five-stage pipeline into two stages:
1. Issue -- Decode instructions, check for structural hazards.
2. Read operands -- Wait until no data hazards, then read operands.

   
An exception is imprecise if the processor state when an exception is raised does not look excetly as if the instructions were executed sequentially in strict program order.
   
The pipeline allows multiple instructions to be in execution at the same time. Having multiple instructions in execution at once requires ***multiple functional units, pipelined functional units, or both***.

   
In a dynamically scheduled pipeline, all instructions pass through the issue stage in order (in-order issue); however, they can be stalled or bypass each other in the second stage (read operands) and thus enter exection out of order.

   
The key concepts of ***Tomasulo's approach*** is tracking instruction dependences to allow execution as soon as operands are available and renaming registers to avoid WAR and WAW hazards. 

   
***Register renaming*** eliminates these hazards by renaming all destination registers, including those with a pending read or write for an earlier instruction, so that the out-of-order write dose not affect any instructions that depend on an earlier value of an operand.
   
In Tomasulo's shceme, register renaming is provided by ***reservation stations***, which fetch and buffers an operand as soon as it is available, eliminating the need to get the operand from a register.

   
The reservation stations include the operation and the actual operands, as well as information used for detecting and resolving hazards (tags).

   
***The tag field*** describes which reservation station contains the instrucion that will produce a result needed as a source operand.

   
The tags in the Tomasulo scheme refer to the buffer or unit that will produce a result; the register names are discarded when an instruction issues to a reservation station.



