# BUG-4

## Category

- [2] Stack Buffer Overflow

## Description

When the length of second argument (`argv[1]`) is longer than `OUTPUT_NAME_SIZE` (500), the method `strcpy` occurs a buffer overflow error. That's because the char array `output_name`'s size is assigned as `OUTPUT_NAME_SIZE`.

## Affected Lines in the original program

In `solid.c:33`.

## Expected vs Observed

When the wrong input (longer than 500 of second argument) comes, the program should print ussage error message, however, the buffer overflow error is detected.

## Steps to Reproduce

### Command

```bash
./solid 1234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567891234567_longer_than_500.png 100 100 123456
```

## Suggested Fix Description

Use `strncpy` instead of `strcpy`.

Raise an error if the `argv[1]` is longer or same with `OUTPUT_NAME_SIZE`, becasue last element of `output_name` should be filled with null terminator. 