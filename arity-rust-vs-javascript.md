# Cheatsheet: Function Arity in Rust vs. Javascript

> ✨ Get the full expert version of this tutorial on my [Patreon page](https://www.patreon.com/posts/beyond-argument-138218742?utm_medium=clipboard_copy&utm_source=copyLink&utm_campaign=postshare_creator&utm_content=join_link).

Don't forget to [watch my associated video](https://youtube.com/shorts/Av64m3LeL48?feature=share).

# Cheatsheet: Function Arity in JavaScript vs. Rust

Function **arity** is the number of arguments a function accepts. How a language handles arity reveals its core philosophy—whether it prioritizes flexibility or strict, compile-time safety. This cheatsheet shows two contrasting approaches using practical examples.

---

## JavaScript: Pragmatic Permissiveness

JavaScript's design prioritizes flexibility, making it easy to get started. It allows functions to be called with a different number of arguments than declared.

### 1. Check a Function's Declared Arity

Use the `.length` property to see how many named parameters a function was declared with.

```javascript
function calculate(price, tax, discount) {
  return price + (price * tax) - discount;
}

// The function expects 3 arguments
console.log(calculate.length);
// Output: 3
```

### 2. Call a Function with a Mismatched Number of Arguments

JavaScript will not error if you provide more or fewer arguments. Missing arguments are `undefined`, and extra arguments are ignored.

```javascript
// Called with fewer arguments (discount is undefined)
calculate(100, 0.2); // Returns NaN (100 + 20 - undefined)

// Called with more arguments (the '4th' is ignored)
calculate(100, 0.2, 10, 'extra'); // Returns 110 (100 + 20 - 10)
```

### 3. Handle a Variable Number of Arguments (Variadic)

Use the **rest parameter (`...`)** to capture an indefinite number of arguments into a single array. This is the modern and preferred approach.

```javascript
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3));    // Output: 6
console.log(sum(10, 20));     // Output: 30
console.log(sum());           // Output: 0
```

---

## Rust: Strict Safety

Rust prioritizes memory safety and predictability. Arity is strictly enforced by the compiler, eliminating an entire class of runtime bugs.

### 1. Define a Function with Fixed Arity

Functions must be called with the exact number and type of arguments they are defined with. Any mismatch will cause a **compile-time error**.

```rust
// This function MUST be called with two i32 integers.
fn add(x: i32, y: i32) -> i32 {
    x + y
}

// This is a valid call:
let result = add(5, 10);
println!("Sum is: {}", result); // Output: Sum is: 15

// This would FAIL TO COMPILE:
// let error_result = add(5);
// error: this function takes 2 arguments but 1 argument was supplied
```

### 2. Handle a Variable Number of Arguments with Slices

Rust does not have traditional variadic functions for safety reasons. Instead, the idiomatic way to pass a sequence of values is by using a **slice (`&[T]`)**.

```rust
// This function accepts a slice of i32 integers.
fn sum_all(numbers: &[i32]) -> i32 {
    numbers.iter().sum()
}

// You can pass an array slice of any length.
let total1 = sum_all(&[1, 2, 3, 4, 5]);
let total2 = sum_all(&[10, 20]);

println!("Total 1: {}", total1); // Output: Total 1: 15
println!("Total 2: {}", total2); // Output: Total 2: 30
```

---

### My Mission

My mission is to help open source creators sustain their projects, both technically and financially. More specifically, it involves helping those who want to make open source a solid development and business model, while preserving its core values. This involves supporting open source entrepreneurs so they can build solid business models that remain true to their values ​​while generating predictable and sustainable revenue. My goal is to help them transform open source into a commercial success, build solid business models, and create solutions that captivate users. I also strive to help those who want to build a real business with open source, while respecting the standards that make it so powerful.

---

### Want to Learn More?

For more tutorials and deep dives into software development and open source strategy, check out my content:

-   **Watch all my videos on YouTube:** [https://www.youtube.com/@herveberaud/](https://www.youtube.com/@herveberaud/)
-   **Get exclusive content and support my work on Patreon:** [patreon.com/herveberaud](https://patreon.com/herveberaud)
