# Hex Dump & Disassembly

## Question  
**“Show me how to turn my ELF into a raw hex and to disassemble it with objdump. What do each of the columns mean?”**

---

## Step-by-Step Method

### 1. Disassemble the ELF file

```bash
riscv32-unknown-elf-objdump -d hello.elf > hello.dump
```

- This command disassembles the binary ELF file into human-readable RISC-V assembly and writes the output into `hello.dump`.

---

### 2. Convert ELF to Intel HEX format

```bash
riscv32-unknown-elf-objcopy -O ihex hello.elf hello.hex
```

- This converts the ELF file to a HEX format, which is a common format used for flashing firmware onto embedded systems.

---

## Understanding the `objdump` Output

A typical disassembly output will look like this:

```
00010074 <main>:
   10074: 1141                 addi    sp,sp,-16
   10076: c606                 sw      ra,12(sp)
   10078: c422                 sw      s0,8(sp)
   1007a: 842a                 mv      s0,sp
   1007c: 00000517             auipc   a0,0x0
   10080: 02050513             addi    a0,a0,32
   10084: 00000097             auipc   ra,0x0
   10088: 000080e7             jalr    ra
```

Each line contains four parts:

| Field        | Description                                                             |
|--------------|--------------------------------------------------------------------------|
| **Address**  | Memory address of the instruction (`10074`, `10076`, etc.)              |
| **Opcode**   | The raw machine code in hexadecimal (`1141`, `c606`, etc.)              |
| **Mnemonic** | The assembly operation (`addi`, `sw`, `mv`, etc.)                       |
| **Operands** | The operands for the instruction (`sp,sp,-16`, `ra,12(sp)`, etc.)       |

---

## Commands Screenshot

![Output Screenshot](Resources/hexdump.png)

---

## Output Text Files
Disassemble Output Text File.
![View Disassembly (hello.dump)](Resources/hello.dump)

Elf into a raw hex Text File.
![View Hex Dump (hello.hex)](Resources/hello.hex)

---
