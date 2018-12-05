Traditionally, ***main memory latency*** (which affects the cache miss penalty) is the primary concern of the cache, while ***main memory bandwidth*** is the primary concern of multiprocessors and I/O.
   
Memory latency is quoted using two measures:
- ***access time*** is the time between when a read is requested and when the desired word arrives.
- ***cycle time*** is the minimum time between unrelated requests to memory.

### SRAM Technology
SRAMs don't need to refresh, so the access time is very close to the cycle time.   

SRAMs typically use six transistors per bit to prevent the information from being disturbed when read.

### DRAM Technology
Multiplex the address lines, thereby cutting the number of address pins in half: first ***row access strobe (RAS)***; second ***column access strobe (CAS)***.   
   
Reading that bit destorys the information, so it must be restored. (This is why its cycle time larger than access time)
   
To prevent loss of information when a bit is not read or written, the bit must be "refreshed" periodically. (By reading that row)
   
Amdahl suggested as a rule of thumb that memory capacity should grow linearly with processor speed to keep a balanced system.
   
DRAMs are commonly sold on small boards called ***dual inline memory modules*** (DIMMs).

### Improving Memory Performance Inside a DRAM Chip
1. DRAMs added timing signals that allow repeated accesses to the row buffer without another row access time.
2. Add a clock signal to the DRAM interface, so that the repeated transfers would not bear the overhead to synchronize with the controller. ***(Synchronous DRAM (SDRAM))***
3. DRAMS were made wider to get a wide stream of bits from the memory without having to make the memory system too large as memory system density increased.
4. Transfer data on both the rising edge and falling edge of the DRAM clock signal, thereby double the peak data rate. ***(double data rate (DDR))***
5. SDRAMs also introduced banks, breaking a single SDRAM into 2 to 8 blocks that can operate independently.

DDR SDRAMs are packaged as DIMMs.
    
GDRAMs or GSDRAMs (Graphics or Graphics Synchronous DRAMs).   
GDDRs (based on graphics RAM and DDR DRAMs) have several important differences:
1. GDDRs have wider interfaces: 32-bits versus 4, 8, or 16 in current designs.
2. GDDRs have a higher maximum clock rate on the data pins.

### Reducing Power Consumption in SDRAMs
Power consumption in dynamic memory chips consists of both dynamic power used in a read or write and static or standby power; both depend on the operating voltage.
   
SDRAMs support a ***power down mode***, which disables the SDRAM, except for internal automatic refresh.

### Flash Memory
Flash memory is a type of EEPROM (Electronically Erasable Programmable Read-Only Memory), which is normally read-only but can be erased and holds it contents without any power.
   
Flash uses a very different architecture and has different properties than standard DRAM:
1. Flash memory must be erased before it is overwritten, and it is erased in blocks.
2. Flash memory is static and draws significantly less power when not reading or writing.
3. Flash memory has a limited number of write cycles for any block.
4. cheap than SDRAM but more expensive than disk.
5. slower than SDRAM but fast than disk.

### Enhancing Dependablility in Memory Systems
Dynamic errors can be detected by three approaches:
- ***parity bits***.
- ***Error Correcting Codes*** (ECCs).
- ***Chipkill*** distributes the data and ECC information, so that the complete failure of a single memory chip can be handled by supporting the reconstruction of the missing data from the remaining memory chips. 

