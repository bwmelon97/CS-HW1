# BUG-2

## Category

- String vulnerability

## Description

The `char` array variable `arg` is assigned its length as `ARG_SIZE`, which is defined as 255.

```c
// filter.c:6
#define ARG_SIZE 255

// filter.c:248
char arg[ARG_SIZE];
```

When program `filter` is executed with 4 arguments, variable `arg` is assigned value of `argv[4]` by method `strcpy` in original version. However, if length of `argv[4]` is larger than `ARG_SIZE`, `argv[4][ARG_SIZE - 1]` is not a null terminator, and the method `strcpy` copies the char array without a null terminator. So, string vulnerability error should occur in `arg`, when forth argument of filter is longer than 255.

## Affected Lines in the original program

In `filter.c:274`

## Expected vs Observed

When we input the forth argument longer than length of 255, and if it is not a valid argument, program should raise usage error, so that let the user know the right usage.

But we observed a segmentation fault, because there are string vulnerability in the process of coping the forth argument.

## Steps to Reproduce

### Command

```bash
./filter poc.png out.png blur 123456789123456789...123456789(longer_than_255_input)
```

### Proof-of-Concept Input (if needed)

(attached: poc.png)

## Suggested Fix Description

Use `strncpy` with length `ARG_SIZE`, instead of `strcpy`. The method `strncpy` with smaller or same length of char array guarantees that the char array ends with a null terminator. 