# BUG-6

## Category

- [11] Type Error

## Description

The type of the second parameter of the method `strtol()` should be `char**`. However, in the original program, the variable `end_ptr` which type is `char*` is given.

## Affected Lines in the original program

In `rect.c:34`.
```c
long hex_color = strtol(argv[7], end_ptr, 16);
```

## Expected vs Observed

When the program is executed with proper arguments, it is expected to work properly. However, Segmentation Fault is observed.

## Steps to Reproduce

### Command

```bash
./rect poc.png output.png 10 10 50 50 123456
```

### Proof-of-Concept Input (if needed)

(attached: poc.png)

## Suggested Fix Description

Modify `end_ptr`, the second variable of `strtol` method to `&end_ptr`.