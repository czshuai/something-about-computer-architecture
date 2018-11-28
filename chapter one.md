# Classes of Parallelism and Parallel Architectures
Two kinds of parallelism in applications:
1. Data-Level Parallelism (DLP)
2. Task-Level Parallelism (TLP)

Computer hardware in turn can exploit these two kinds of application parallelism in four major ways:
1. Instruction-Level Parallelism (DLP)
2. Vector Architectures and Graphic Processor Units (DLP)
3. Thread-Level Parallelism (DLP/TLP)
4. Request-Level Parallelism (TLP)

another taxonomy:
1. Single instruction stream, single data stream (SISD) : uniprocessor
2. Single instruction stream, multiple data stream (SIMD) : The same instruction is executed by multiple processors using different data streams.
3. Multiple instruction streams, single data stream (MISD)
4. Multiple instruction streams, multiple data streams (MIMD) : Each processor fetches its own instructions and operates on its own data.
---
# Defining Computer Architecture
The word  ***architecture***  covers three aspects of computer design -- **instruction set architecture, organization or microarchitecture, and hardware**. 

- Organization(microarchitecture) : Including the high-level aspects of a computer's design.
- Hardware : Refering to the specifics of a computer. 
---
# Energy and Power within a Microprocessor
Primary evaluation now is tasks per joule or performance per watt.

---
# The Processor Performance Equation

Instruction Count （IC）
Clock cycles per instruction (CPI)
> CPU time = Instruction count * Cycles per instruction * Clock cycle time

At this formula demonstrates, processor performance is dependent upon three characteristics: **clock cycle (or rate), clock cycles per instruction, and instruction count**.



