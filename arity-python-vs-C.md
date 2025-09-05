# Cheatsheet: Function Arity in Python vs. C

*For the full expert version of this tutorial, including advanced techniques and deeper insights is available on my [Patreon](https://www.patreon.com/posts/understanding-vs-138208997?utm_medium=clipboard_copy&utm_source=copyLink&utm_campaign=postshare_creator&utm_content=join_link)*

**Arity** — the number of arguments a function accepts — reveals a language's core philosophy. This cheatsheet explores two opposing approaches: Python's dynamic flexibility versus C's strict, compile-time control.

Don't forget to [watch my associated video](https://youtube.com/shorts/Av64m3LeL48?feature=share).

---

### 🐍 Python — Dynamic Flexibility

Python prioritizes adaptability. Arity is flexible and can be determined at runtime. You can define functions that accept an unlimited number of arguments using star-args (`*args`).

**Example: Inspecting Arity and Using Star-Args**

Use the `inspect` module to check a function's signature at runtime, and `*args` to handle a variable number of arguments.

```python
import inspect

# A function with a fixed arity of 2
def add(a, b):
    return a + b

# A function with variable arity via star-args
def sum_all(*args):
    return sum(args)

# Inspect the signature at runtime
print("Arity of add:", len(inspect.signature(add).parameters))
# > Arity of add: 2

# Call the function with a dynamic number of arguments
print("Dynamic call:", sum_all(1, 2, 3, 4))
# > Dynamic call: 10
```

---

### 🔧 C — Strict Control

C prioritizes performance and explicit control. Arity is fixed and checked at compile time. While variadic functions are possible using `<stdarg.h>`, the developer is responsible for manually and safely reading the arguments from the stack.

**Example: Fixed Arity and Manual Variadic Functions**

This code demonstrates a standard function with fixed arity and a variadic function where the argument count must be passed manually.

**C Code (`demo.c`)**
```c
#include <stdarg.h>
#include <stdio.h>

// Fixed arity, known at compilation
int add(int a, int b) {
    return a + b;
}

// Variadic function, manually managed
int sum_all(int count, ...) {
    va_list args;
    va_start(args, count); // Initialize arg list
    int s = 0;
    for (int i = 0; i < count; i++) {
        // Read arguments sequentially from the stack
        s += va_arg(args, int);
    }
    va_end(args); // Clean up
    return s;
}

int main(void) {
    printf("Fixed arity: %d\n", add(2, 3));
    printf("Manual variadic: %d\n", sum_all(4, 1, 2, 3, 4));
}
```

**Compile and Run**

Use this command to compile the C code from standard input, execute it, and clean up.

```bash
gcc -x c -std=c11 -O2 -o /tmp/prog - <<'C'
#include <stdarg.h>
#include <stdio.h>
// ... Paste the C code from above here ...
int main(void) {
    printf("Fixed arity: %d\n", add(2, 3));
    printf("Manual variadic: %d\n", sum_all(4, 1, 2, 3, 4));
}
C
/tmp/prog
rm -f /tmp/prog

# Output:
# Fixed arity: 5
# Manual variadic: 10
```

### Key Takeaways

*   **🎯 Two Philosophies:** Python and C represent two extremes in function design.
*   **🔄 Python:** Offers dynamic, flexible arity with runtime introspection.
*   **⚡ C:** Enforces static, controlled arity for performance and low-level management.

***

### My Mission

My mission is to help open source creators sustain their projects, both technically and financially. More specifically, it involves helping those who want to make open source a solid development and business model, while preserving its core values. This involves supporting open source entrepreneurs so they can build solid business models that remain true to their values while generating predictable and sustainable revenue. My goal is to help them transform open source into a commercial success, build solid business models, and create solutions that captivate users. I also strive to help those who want to build a real business with open source, while respecting the standards that make it so powerful.

***

Want to see more tutorials like this? Check out the companion video and other deep dives on my channel!

➡️ **Watch all my videos on YouTube:** [https://www.youtube.com/@herveberaud/](https://www.youtube.com/@herveberaud/)

➡️ **Support my work and get exclusive content on Patreon:** [patreon.com/herveberaud](https://patreon.com/herveberaud)
