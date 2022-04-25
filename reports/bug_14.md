# BUG-14

## Category

- [10] Wrong Operator

## Description

`new_img->px` should be allocated size of (number of pixels) * (size of struct pixel). But in the original program, it is allocated size of (number of pixels) + (size of struct pixel).


## Affected Lines in the original program

In `resize.c:48`

```c
new_img->px = malloc(n_pixels + sizeof(struct pixel));
```

## Expected vs Observed

We observed an segmentation fault.

## Steps to Reproduce

### Command

```bash
./resize poc.png output.png 3
```

### Proof-of-Concept Input (if needed)

(attached: poc.png)

## Suggested Fix Description

Modify `+` to `*`.

```c
new_img->px = malloc(n_pixels * sizeof(struct pixel));
```

