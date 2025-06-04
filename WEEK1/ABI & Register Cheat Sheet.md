# 5. ABI & Register Cheat-Sheet

## 📌 Question

**“List all 32 RV32 integer registers with their ABI names and typical calling-convention roles.”**

---

## 🧾 Register Table

| Register | ABI Name | Role in Calling Convention     |
| -------- | -------- | ------------------------------ |
| x0       | zero     | Hardwired zero                 |
| x1       | ra       | Return address                 |
| x2       | sp       | Stack pointer                  |
| x3       | gp       | Global pointer                 |
| x4       | tp       | Thread pointer                 |
| x5       | t0       | Temporary (caller-saved)       |
| x6       | t1       | Temporary (caller-saved)       |
| x7       | t2       | Temporary (caller-saved)       |
| x8       | s0/fp    | Saved register / frame pointer |
| x9       | s1       | Saved register (callee-saved)  |
| x10      | a0       | Argument / return value        |
| x11      | a1       | Argument / return value        |
| x12      | a2       | Argument                       |
| x13      | a3       | Argument                       |
| x14      | a4       | Argument                       |
| x15      | a5       | Argument                       |
| x16      | a6       | Argument                       |
| x17      | a7       | Argument                       |
| x18      | s2       | Saved register (callee-saved)  |
| x19      | s3       | Saved register (callee-saved)  |
| x20      | s4       | Saved register (callee-saved)  |
| x21      | s5       | Saved register (callee-saved)  |
| x22      | s6       | Saved register (callee-saved)  |
| x23      | s7       | Saved register (callee-saved)  |
| x24      | s8       | Saved register (callee-saved)  |
| x25      | s9       | Saved register (callee-saved)  |
| x26      | s10      | Saved register (callee-saved)  |
| x27      | s11      | Saved register (callee-saved)  |
| x28      | t3       | Temporary (caller-saved)       |
| x29      | t4       | Temporary (caller-saved)       |
| x30      | t5       | Temporary (caller-saved)       |
| x31      | t6       | Temporary (caller-saved)       |

---

## 🧠 Summary of Calling Convention

* **`a0`**\*\* – \*\***`a7`** → Function arguments and return values
* **`s0`**\*\* – \*\***`s11`** → Saved registers (callee-saved)
* **`t0`**\*\* – \*\***`t6`** → Temporaries (caller-saved)
* **`ra`** → Return address (set by `call`)
* **`sp`** → Stack pointer (manages function stack frame)
* **`fp`** → Frame pointer (alias for `s0`)

---

