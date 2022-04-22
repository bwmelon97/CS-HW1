# BUG-8

## Category

- [9] Iteration Error

## Description

The variable `i` and `j` is iterator variables of while loop, and `i` is for vertical (y-index) and `j` is for horizontal (x-index). The inner while loop is about horizontal (x-index), so that the value of `i` should not increase in the inner loop and should increase in the outer loop.


## Affected Lines in the original program

In range `rect.c:80` to `rect.c:83`.
```c
  while (i < height) {      // line 63
    while (j < width) {
      ...
      i++;                  // line 80. This line should be moved to outer loop.
      j++;
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

Move `i++;` to outer loop. That means move 'line 80' to 'line 82'.