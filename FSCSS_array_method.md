# FSCSS Array Methods
**For version 1.1.14+**

>Arrays for scalable CSS generation.

---

## Overview

FSCSS arrays are data structures designed to generate CSS efficiently. Unlike traditional script arrays, FSCSS arrays return strings directly, making them ideal for reducing repetition and generating utility patterns at compile time.

### Key Characteristics
- **String-native** – All transformations output final string values
- **No method chaining** – Arrays return directly, not objects
- **No nested execution** – Array declarations don't resolve inner arrays

---

## Array Declaration

```fscss
@arr name[item1, item2, item3]
```

Example

```fscss
@arr colors[#1E2783, #8C29B2, #C41348]
@arr spacing[4, 8, 12, 16]
@arr variants[primary, secondary, accent]
```

---

Access Modes

Direct Output (Space Separated)

```fscss
@arr.name
// Returns: item1 item2 item3
```

Method Access Mode

Append ! to enable method calls:

```fscss
@arr.name!
// Enables: @arr.name!.reverse, @arr.name!.length, etc.
```

---

Available Methods

| Method | Description | Example | Output |
|---|---|---|---|
| .length | Returns number of items | @arr.n!.length | 3 |
| .first | Returns first item | @arr.n!.first | item1 |
| .last | Returns last item | @arr.n!.last | item3 |
| .list | Comma-separated list | @arr.n!.list | item1,item2,item3 |
| .join(sep) | Join with custom separator | @arr.n!.join(+) | item1+item2+item3 |
| .reverse | Reverse order (comma list) | @arr.n!.reverse | item3,item2,item1 |
| .shuffle | Random order (comma list) | @arr.n!.shuffle | item2,item3,item1 |
| .sort | Alpha/numeric sort | @arr.n!.sort | item1,item2,item3 |
| .unique | Remove duplicates | @arr.n!.unique | item1,item2,item3 |
| .indices | 1-based indices | @arr.n!.indices | 1,2,3 |
| .randint | Returns a random item | @arr.n!.randint | item2 |
| .segment | Wrap in [] brackets | @arr.n!.segment | [item1][item2][item3] |
| .sum | Sum numeric values | @arr.num!.sum | 15 |
| .min | Minimum numeric value | @arr.num!.min | 4 |
| .max | Maximum numeric value | @arr.num!.max | 16 |
| .unit(val) | Append unit to each | @arr.n!.unit(px) | 4px,8px,12px |
| .prefix(v) | Add prefix to each | @arr.b!.prefix(btn-) | btn-A,btn-B,btn-C |
| .surround(b,a) | Wrap each item | @arr.b!.surround([,]) | [A][B][C] 

---

Array Mutation

Add Items

```fscss
@arr.name!+[item4, item5]
```

Remove Item (1-based index)

```fscss
@arr.name!-[2] // Removes second item
```

---

Important Limitations

❌ No Method Chaining

The following will not work:

```fscss
@arr.name!.unit(px)!.join(+) // Invalid
```

Each method returns a string, not an array object.

❌ No Nested Array Execution

The following will not resolve the inner array:

```fscss
@arr.b[@arr.a!.list] // Stores literal string, doesn't execute
```

---

Design Philosophy

FSCSS arrays are intentionally constrained to excel at their primary purpose:

· String-output generators – Direct transformation to CSS values
· Repetition reducers – Eliminate manual duplication
· Utility pattern generators – Create systematic CSS variations

This focused approach ensures predictable, performant CSS generation without the complexity of full scripting capabilities.

---

Practical Examples

Gradient Generator

```fscss
@arr colors[#1E2783, #8C29B2, #C41348]

.box {
  background: linear-gradient(40deg, @arr.colors!.list);
}
/* Output: background: linear-gradient(40deg, #1E2783,#8C29B2,#C41348); */
 
.box-2 {
  background: linear-gradient(40deg, @arr.colors!.reverse);
}
/* Output: background: linear-gradient(40deg,#C41348,#8C29B2,#1E2783); */
```

Spacing Utilities

```fscss
@arr spaces[4, 8, 12, 16, 24]

.m-@arr.spaces[] {
  margin: @arr.spaces[]px;
}
```

Component Variants

```fscss
@arr colors[#0066FF, #6B7280, transparent]

.btn-a {
  background: @arr.colors!.randint;
}
.btn-b {
  background: @arr.colors!.randint;
}
```

Reducing Typing with %n() Loop

```fscss
@arr sizing[width, height, max-width, max-height, min-height, min-width];
  
/* store array reference */
$sizing: @arr.sizing!;
  
.box {
  %6($sizing.list[: 200px;])
}
/* Output: 
width: 200px; 
height: 200px; 
max-width: 200px; 
max-height: 200px; 
min-height: 200px; 
min-width: 200px;
*/
```

---

Best Practices

1. Use method access mode (!) only when needed – Direct output suffices for simple inclusion
2. Plan array structure before methods – Design arrays for their intended transformations
3. Keep arrays focused – Single-purpose arrays are more maintainable
4. Combine with other FSCSS features – Arrays work well with variables, loops and utility generators

---

Why FSCSS Arrays?

Feature Benefit
String-native Predictable CSS output
Simple syntax Minimal learning curve
Focused methods Purpose-built for CSS
Direct output Easy debugging

---

**Summary**

FSCSS arrays provide a pragmatic approach to data structures for CSS generation. By embracing their limitations—no chaining, no nesting—they deliver reliable, readable, and maintainable style systems.

**Use them to:**

- Generate color palettes and gradients
- Create systematic spacing scales
- Build component variant systems
- Manage responsive breakpoints
- Reduce manual repetition

**Avoid them for:**

- Complex data manipulation
- Nested data structures

---

*FSCSS arrays: Simple by design, powerful in practices*

