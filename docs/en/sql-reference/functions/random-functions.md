---
toc_priority: 51
toc_title: Generating Pseudo-Random Numbers
---

# Functions for Generating Pseudo-random Numbers {#functions-for-generating-pseudo-random-numbers}

Non-cryptographic generators of pseudo-random numbers are used.

All the functions accept zero arguments or one argument.
If an argument is passed, it can be any type, and its value is not used for anything.
The only purpose of this argument is to prevent common subexpression elimination, so that two different instances of the same function return different columns with different random numbers.

## rand {#rand}

Returns a pseudo-random UInt32 number, evenly distributed among all UInt32-type numbers.
Uses a linear congruential generator.

## rand64 {#rand64}

Returns a pseudo-random UInt64 number, evenly distributed among all UInt64-type numbers.
Uses a linear congruential generator.

## randConstant {#randconstant}

Produces a constant column with a random value.

The function is intended for service purposes.

**Syntax**

``` sql
randConstant(x)
```

**Parameters**

-   `x` — optional expression. Its value is ignored and used only for [Common Subexpression Elimination](index.md#common-subexpression-elimination).

**Returned value**

-   Pseudo-random number.

Type: [UInt32](../data_types/int_uint.md).

**Examples**

Query:

``` sql
SELECT randConstant() >= 0
```

Result:

``` text
┌─greaterOrEquals(randConstant(), 0)─┐
│                                  1 │
└────────────────────────────────────┘
```

Query:

``` sql
SELECT randConstant(), randConstant()
```

Result:

``` text
┌─randConstant()─┬─randConstant()─┐
│     2481280514 │     2481280514 │
└────────────────┴────────────────┘
```

Query:

``` sql
SELECT randConstant(1), randConstant(2)
```

Result:

``` text
┌─randConstant(1)─┬─randConstant(2)─┐
│      4115618163 │      1307298351 │
└─────────────────┴─────────────────┘
```

[Original article](https://clickhouse.tech/docs/en/query_language/functions/random_functions/) <!--hide-->
