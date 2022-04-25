# BUG-11

## Category

- [4] Arithmetic overflow / underflow

## Description

The value of variable `color1`, `color2` should be in range of `0x000000` ~ `0xffffff` (Only positive value). However, if the negative value, such as `-12345` is given, the original program recognizes it as negative complement (`0xfffedcba`).


## Affected Lines in the original program

In range `checkerboard.c:49` to `checkerboard.c:59`.

```c
long color1 = strtol(hex_color_arg1, &end_ptr, 16);
if (*end_ptr) {
    goto error;
}

long color2 = strtol(hex_color_arg2, &end_ptr, 16);
if (*end_ptr) {
    goto error;
}
```

## Expected vs Observed

When the negative value is given for 6th, and 7th arguments, which is `color1`, `color2`, The program is expected to raise an usage error so that prompt the user to enter the appropriate input. However, if the negative value's length is 6 (contains `-`), the original program recognize it as a negative complement value.

## Steps to Reproduce

### Command

```bash
./checkerboard output.png 100 200 10 -12345 654321
```

## Suggested Fix Description

Check the value of the variable `color1`, and `color2` are negative. And if they are negative, raise an usage error.

```c
  long color1 = strtol(hex_color_arg1, &end_ptr, 16);
  if (*end_ptr || color1 < 0) {
    goto error;
  }

  long color2 = strtol(hex_color_arg2, &end_ptr, 16);
  if (*end_ptr || color2 < 0) {
    goto error;
  }
```

