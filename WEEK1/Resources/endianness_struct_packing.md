
## 17 Endianness & Struct Packing

---

### **Question**  
**“Is RV32 little-endian by default? Show me how to verify byte ordering with a union trick in C.”**

---

### **Method**  
- Use a union containing `uint32_t` and a byte array `uint8_t[4]`.
- Store a known value like `0x01020304`.
- Print each byte to inspect the order in memory.

---

### 🧪 Example C Code

```c
#include <stdio.h>
#include <stdint.h>

int main() {
    union {
        uint32_t word;
        uint8_t bytes[4];
    } u;

    u.word = 0x01020304;

    for (int i = 0; i < 4; i++) {
        printf("Byte %d: 0x%02x\n", i, u.bytes[i]);
    }

    return 0;
}
```

---

### 🔍 Expected Output on RV32 (Little-Endian)
```
Byte 0: 0x04
Byte 1: 0x03
Byte 2: 0x02
Byte 3: 0x01
```

---

### ✅ Interpretation
- **RV32 is little-endian**, so the least significant byte (0x04) appears first in memory.
- This union trick is a simple and effective way to observe byte ordering directly.

---

### 🛠️ Build Command
```sh
riscv32-unknown-elf-gcc -o endian_test.elf endian_test.c
```

---

