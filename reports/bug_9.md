# BUG-9

## Category

- [5] Heap Overflow

## Description

The length of `argv[]` is 7. Therefore, trying to access 8 index of `argv`,  `argv[7]`, will occur heap Overflow.


## Affected Lines in the original program

In range `circle.c:29` to `circle.c:30`.
```c
long hex_color = strtol(argv[7], &end_ptr, 16);
if (*end_ptr || strlen(argv[7]) != 6 || hex_color < 0) { ... }
```

## Expected vs Observed

When the program is executed with proper arguments, it is expected to work properly.  However, we observed a segmentation fault.

## Steps to Reproduce

### Command

```bash
./circle test_imgs/desert.png output.png 75 75 50 123456
```

### Proof-of-Concept Input (if needed)

(attached: poc.png)

## Suggested Fix Description

We can solve this bug by modifying `argv[7]` -> `argv[6]`, which is the value of hex_color.