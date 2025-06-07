# Question:
“Provide a two-thread mutex example (pseudo-threads in main) using `lr.w` / `sc.w` on RV32.”

# Method:
- Simulate two threads using functions in `main`.
- Use `lr.w` / `sc.w` instructions in inline assembly for a spinlock mutex.
- Demonstrate protection of a shared variable (`shared_counter`) from race conditions.

# Full Code with Explanation:

```c
#include <stdint.h>
#include <stdio.h>

volatile int lock = 0;
volatile int shared_counter = 0;

void acquire_lock(volatile int* lock) {
    int tmp;
    do {
        __asm__ volatile (
            "lr.w %[tmp], (%[lock])\n"
            "bnez %[tmp], 1f\n"
            "li %[tmp], 1\n"
            "sc.w %[tmp], %[tmp], (%[lock])\n"
            "1:"
            : [tmp] "=&r"(tmp)
            : [lock] "r"(lock)
            : "memory"
        );
    } while (tmp != 0);
}

void release_lock(volatile int* lock) {
    __asm__ volatile (
        "sw zero, 0(%[lock])"
        :
        : [lock] "r"(lock)
        : "memory"
    );
}

void thread1() {
    acquire_lock(&lock);
    shared_counter += 1;
    printf("Thread 1 incremented counter to %d\n", shared_counter);
    release_lock(&lock);
}

void thread2() {
    acquire_lock(&lock);
    shared_counter += 1;
    printf("Thread 2 incremented counter to %d\n", shared_counter);
    release_lock(&lock);
}

int main() {
    for (int i = 0; i < 5; ++i) {
        thread1();
        thread2();
    }
    return 0;
}
```

# Expected Output:
```text
Thread 1 incremented counter to 1
Thread 2 incremented counter to 2
Thread 1 incremented counter to 3
Thread 2 incremented counter to 4
Thread 1 incremented counter to 5
Thread 2 incremented counter to 6
...
```

# Concepts:
- **Spinlock**: A busy-wait loop that tries acquiring a lock until it succeeds.
- **lr.w / sc.w**: RISC-V atomic instructions used for load-reserved and store-conditional, ensuring safe memory access without interference.
- **Volatile**: Prevents the compiler from optimizing or caching memory accesses.
- **Pseudo-threads**: Simulating threads using functions in `main` to demonstrate mutex usage.
