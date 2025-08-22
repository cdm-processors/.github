## Coco de Mare CPU family

CdM is a family of 8- and 16-bit CPU implemented in logical circuit emulator tool [Logisim](https://cburch.com/logisim/).  

These processors are intended for hobby and educational projects involving a hardware-software co-design.  You can insert 
the CPU chip in Logisim circuit, add RAM and ROM chips, some peripherials ranging from built-in Logisim terminal to custom designed displays with memory mapped videobuffer or floating point `hardware' accelerators, upload software and build anything your imagination allows.  For the debugging, in-circuit debugger chip is available.

These are fully functional (as much as you can expect from von-Neuman CPU with 8- and 16-bit address space) Load-Store processors with microprogrammed internal architecture and development tools, including standalone software emulators, macroassembler, 
linker, debugger, VsCode plugins and, for CdM-16, even LLVM-based C compiler (Work In Progress).

Due to low performance of Logisim with large circuits (and CdM-16 CPU is large by Logisim standards) we implemented the JAR plugin
for the Logisim with software emulated CdM-16 chip.  This plugin shares the code with standalone software emulator and the microcode
with 'hardware' implementation.

Both CdM-8 and CdM-16 support memory mapped I/O, von-Neuman and Harvard memory layouts and vectored external interrupts.  CdM-16 also supports internally and externally triggered exceptions. External exceptions are intended for possible future addition of MMU and coprocessors.

Datasheet (GPR stands for General Purpose Register):

| CPU  |Data path|GPR|addressable code|addressable data|von-Neuman|Harvard|interrupt vectors          |
|------|---------|---|----------------|----------------|----------|-------|---------------------------|
|CdM-8 | 8 bit   | 4 | 256 bytes      | 256 bytes      | yes      | yes   | 8 (Harvard-mode only)     |
|CdM-8e| 8 bit   | 4 | 64k bytes      | 256 bytes      | no       | yes   | 8                         |
|CdM-16| 16 bit  | 8 | 64k bytes      | 64k bytes      | yes      | yes   | 256 (incl. 16 exceptions) |

In addition to general purpose registers, all CdM CPUs have Processor State, Program Counter and Stack Pointer registers.
