# BUG-7

## Category

- [9] Iteration Error

## Description

The variable `i` and `j` is iterator variables of while loop, and `i` is for vertical (y-index) and `j` is for horizontal (x-index). The outer while loop is about vertical (y-index) so that the value of `j` should be initialzed when the outer while loop is start.


## Affected Lines in the original program

In range `rect.c:63` to `rect.c:64`.
```c
while (i < height) {
    // initializing 'j' is missing.
    while (j < width) {
    }
}
```

## Expected vs Observed

When the program is executed with proper arguments, it is expected to work properly. Which means the rectangle with hex_color in the area between TL and BR should be created. However, there are not any changes on output file from original image.

## Steps to Reproduce

### Command

```bash
./rect poc.png output.png 10 10 50 50 123456
```

### Proof-of-Concept Input (if needed)

(attached: poc.png)

## Suggested Fix Description

Add a line for initializing value of variable `j` to `0` between outer while loop and inner while loop.