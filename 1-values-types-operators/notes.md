# Eloquent JavaScript — Chapter 1: Values, Types, and Operators

Source: https://eloquentjavascript.net/01_values.html

## Big idea

- Everything a program manipulates is **data**, stored as **bits**.
- JavaScript groups bits into **values**.
- Every value has a **type**, which affects what you can do with it.

---

## Values

- A **value** is a chunk of information (e.g., `13`, `"hello"`, `true`).
- Values live somewhere (memory). When nothing uses them anymore, their memory can be reused.

---

## Numbers

- JavaScript numbers are stored using **64 bits** (floating point).
- Integers are exact up to a very large range, but **fractional math is approximate**.

### Writing numbers

```js
13
9.81
2.998e8   // scientific notation
```

### Arithmetic operators

- `+` add  
- `-` subtract / negate (binary or unary)  
- `*` multiply  
- `/` divide  
- `%` remainder (“modulo”)

### Operator precedence (practical)

- `*`, `/`, `%` happen before `+`, `-`
- Same-precedence operators evaluate left-to-right
- When in doubt: **use parentheses**

```js
100 + 4 * 11      // 144
(100 + 4) * 11    // 1144
```

### Special numbers

- `Infinity`, `-Infinity`: results of overflow-ish operations (e.g., very large divisions)
- `NaN` (“not a number”): nonsensical numeric result (`0/0`, `Infinity - Infinity`, `"five" * 2`)
- `NaN` is **not equal to itself**

```js
NaN == NaN // false
```

---

## Strings

Strings represent text. You can write them with:

- double quotes: `"text"`
- single quotes: `'text'`
- backticks: `` `text` `` (template literal)

### Escaping

Backslash `\` gives special meaning to the next character.

```js
"This is line 1
This is line 2"
"A newline is written like "\n"."
```

### Unicode + “characters”

- JavaScript strings are based on Unicode.
- Internally, JavaScript uses **16-bit elements**, so some characters (like many emoji) take **two positions** in a string.

---

## Operators: unary, binary, ternary

- **Unary**: operates on 1 value (e.g., `typeof`, `!`, unary `-`)
- **Binary**: operates on 2 values (e.g., `+`, `*`, `==`, `&&`)
- **Ternary**: operates on 3 values (the conditional operator `?`)

### `typeof`

Produces the type name as a string.

```js
typeof 4.5   // "number"
typeof "x"   // "string"
```

---

## Booleans

Boolean values: `true` and `false`.

### Comparisons

- `<`, `>`, `<=`, `>=`, `==`, `!=`

```js
3 > 2      // true
3 < 2      // false
```

String comparisons compare character-by-character using Unicode order, which can be surprising:

- uppercase compares “less than” lowercase (`"Z" < "a"` is true)

### Equality: `==` vs `===`

- `==` allows **type coercion** (automatic conversion)
- `===` checks **strict equality** (no type conversions)

```js
"" == false   // true  (coercion)
"" === false  // false (strict)
```

Special case with `==`:

- `null == undefined` is true
- but `null == 0` is false

---

## Logical operators + truthiness

- `&&` AND
- `||` OR
- `!` NOT

### Precedence

`||` (lowest) → `&&` → comparisons (`==`, `<`, …) → arithmetic

### Conditional (ternary) operator

```js
condition ? valueIfTrue : valueIfFalse
```

---

## Automatic type conversion (coercion)

When an operator gets “the wrong type”, JavaScript often converts values to make it work:

```js
8 * null      // 0
"5" - 1       // 4
"5" + 1       // "51"
"five" * 2    // NaN
false == 0    // true
```

**Default to `===` / `!==` unless you specifically want coercion.**

---

## Short-circuiting + value-returning logic

`&&` and `||` don’t necessarily return booleans — they return **one of the original operands**.

### `||` fallback behavior

- returns left side if it’s “truthy”, otherwise right side

```js
null || "user"      // "user"
"Agnes" || "user"   // "Agnes"
```

The chapter calls out that `0`, `NaN`, and `""` count as false when coerced to boolean:

```js
0 || -1     // -1
"" || "!?"  // "!?"
```

### `??` (nullish coalescing)

- like `||`, but only falls back when the left side is `null` or `undefined`

```js
0 || 100    // 100
0 ?? 100    // 0
null ?? 100 // 100
```

### Short-circuit evaluation

- `true || X` never evaluates `X`
- `false && X` never evaluates `X`
- `?:` also evaluates only the chosen branch

---

## Notes

- Floating point is approximate
- `+` is overloaded: numeric add **or** string concatenation.
- Prefer `===` / `!==` to avoid coercion mistakes.
- `||` / `&&` return operands, and they short-circuit.
