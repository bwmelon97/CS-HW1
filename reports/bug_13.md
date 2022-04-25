# BUG-13

## Category

- [6] Temporal Memory Safety Violation

## Description

When `px` of `img` couldn't be allocated in the memory, the pointer `img` is free on line 91, which is in `if` statement, and on line 145, which is in `error_img:` block. And this occurs a double free error.


## Affected Lines in the original program

In `checkerboard.c:91`

```c
img->px = malloc(sizeof(struct pixel) * n_pixels);
if (!img->px) {
    free(img);		// line 91
    goto error_img;
}
```

## Expected vs Observed

When px of img couldn't be allocated in the memory, double free error occurs in the original program.

```bash
free(): double free detected in tcache 2
Aborted (core dumped)
```

## Steps to Reproduce

### Command

```bash
./checkerboard output.png 50000 50000 200 123456 654321
```

## Suggested Fix Description

Delete the statement `free(img)`.

```c
img->px = malloc(sizeof(struct pixel) * n_pixels);
if (!img->px) {
    goto error_img;
}
```

