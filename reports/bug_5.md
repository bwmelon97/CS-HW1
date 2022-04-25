# BUG-5

## Category

- [3] Command Injection

## Description

In the original code, when the program prints the size of created file, it use `system()` method with `command`. And it has a vulnerability.

## Affected Lines in the original program

In range `solid.c:115` to `solid.c:125`.

## Expected vs Observed

It is not observed in functionality, but it has a vulnerability using `system()` method.

## Steps to Reproduce

### Command

```bash
./solid output.png 100 100 123456
```

## Suggested Fix Description

Get information of file's size by methods related with file (`fopen`, `fseek`, `ftell`, `fclose`), instead of using system method with command.