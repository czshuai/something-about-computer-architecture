There are two largely separable approaches to exploiting ILP:
 1. An approach that relies on hardware to help discover and exploit the parallelism dynamically.
 2. An approach that relies on software technology to find parallelism statically at compile time.
 
   
The value of the CPI for a pipelined processor is the sum of the base CPI and all contributions from stalls:

 > Pipeline CPI = Ideal pipeline CPI + Structural stalls + Data hazard stalls + Control stalls
 
## Data Dependences and Hazards
There are three different types of dependences：data dependences (also called true data dependences), name dependences, and control dependences.
### Data Dependences
An instruction j is data dependent on instruction i if either of the following holds:
 - Instruction i produces a result that may be used by instruction j.
 - Instruction j is data dependent on instruction k, and instruction k is data dependent on instruction i.
   
Dependences are a property of ***programs***.
Whether a given dependence results in an actual hazard being detected and whether that hazard actually causes a stall are properties of the pipeline ***organization***.
   
A data dependence conveys three things:
 1. The possibility of a hazard.
 2. The order in which results must be calculated.
 3. An upper bound on how much parallelism can possibly be exploited.

    
A dependence can be overcome in two different ways:
 1. Maintaining the dependences but avoiding a hazard.
 2. Eliminating a dependence by transforming the code.

### Name Dependences
A name dependence occurs when two instructions use the **same register or memory location**, called a **name**, but there is no flow of data between the instructions associated with that name.
    
There are two types of name dependences between an instrction i that precedes instruction j in program order:
 1. An ***antidependence*** between instruction i and instruction j occurs when instruction j writes a register or memory location that instruction i reads.
 2. An ***output dependence*** occurs when instruction i and instruction j write the same register or memory location.

### Data Hazards 
Data hazards may be classified as one of three types, depending on the order of read and write accesses in the instructions. Consider two instructions i and j, with i preceding j in program order.
 - RAW (read after write): j tries to read a source before i writes it, so j incorrectly gets the old value.
 - WAW (write after write): j tries to write an operand before it is written by i.
 - WAR (write after read): j tries to write a destination before it is read by i, so i incorrectly gets the new value.

### Control Dependences
The two properties critical to program correctness--and normally preserved by maintaining both data and control dependences--are ***the exception behavior*** and ***the data flow***.
   
    

