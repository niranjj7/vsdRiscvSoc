# 9 Inline Assembly Basics

## 🔧 Question
**“Write a C function that returns the cycle counter by reading CSR 0xC00 using inline asm; explain each constraint.”**

---

## 🧪 Method & Example

```c
static inline uint32_t rdcycle(void) {
    uint32_t c;
    asm volatile ("csrr %0, cycle" : "=r"(c));
    return c;
}
```

---

## 🧠 Explanation

### ✅ `static inline`
- `inline` tells the compiler to embed this function wherever it's used instead of calling it—reducing function call overhead.
- `static` limits the function’s scope to the current file, avoiding naming conflicts during linking.

---

### ⚙️ Inline Assembly: `asm volatile (...)`

- `asm` lets you embed assembly code directly in C.
- `volatile` tells the compiler **not to optimize or remove** this statement, even if the result is unused—it **must always run**, crucial for reading real hardware state like cycle counters.

---

### 🔍 `"csrr %0, cycle"`
- `csrr` is an instruction that reads a **CSR (Control and Status Register)**.
- `cycle` is an alias for CSR **0xC00**, which holds the number of cycles since the CPU started.
- `%0` is a placeholder that will be replaced by a register name chosen by the compiler (via constraints).

---

### 🔩 Output Constraint: `: "=r"(c)`

- This is the **output operand** section of the inline assembly.
- `"=r"` is a **constraint**:
  - `"="`: This operand is **write-only** (i.e., output).
  - `"r"`: Use any **general-purpose register**.
- `(c)`: The output will be stored in the C variable `c`.

---

### Summary Table

| Element              | Meaning                                 |
|----------------------|------------------------------------------|
| `asm volatile`       | Don't optimize away; always emit this asm |
| `"csrr %0, cycle"`   | RISC-V CSR read from `cycle` into %0     |
| `: "=r"(c)`          | Output in register → stored in `c`       |
