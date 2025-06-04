# 🛠️ RISC-V Toolchain Setup Guide (rv32imac)

This guide explains how to **install**, **configure**, and **verify** the RISC-V toolchain for the `rv32imac` ISA on a Linux system.

## 📦 Step 1: Download the Toolchain

Download the RISC-V prebuilt toolchain archive (example link):

```bash
wget https://example.com/riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz
```

> Replace the above URL with the actual source of the toolchain you downloaded.

## 📂 Step 2: Extract the Archive

```bash
cd ~/Downloads
tar -xzf riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz -C ~/
```

This will extract the toolchain to your home directory (`~/`).

## 🔧 Step 3: Add to PATH

Edit your `.bashrc` file:

```bash
nano ~/.bashrc
```

Add the following line at the end:

```bash
export PATH=$HOME/riscv/bin:$PATH
```

> If your extracted folder name is different (e.g., `riscv-toolchain`), replace `riscv` accordingly.

Apply the updated environment:

```bash
source ~/.bashrc
```

## ✅ Step 4: Sanity Check

Verify if the toolchain is correctly installed by checking the versions of the binaries:

```bash
riscv32-unknown-elf-gcc --version
riscv32-unknown-elf-objdump --version
riscv32-unknown-elf-gdb --version
```
[Output Screenshot](Resources/gcc.png)
[Output Screenshot](Resources/objdump.png)
[Output Screenshot](Resources/gdb.png)

You should see version output for each of the above commands.

## 🧠 Troubleshooting

- If commands are **not found**, ensure:
  - The correct folder was extracted
  - The `bin/` directory exists
  - The path was correctly added to `.bashrc`
- Restart the terminal or run `source ~/.bashrc` after editing

