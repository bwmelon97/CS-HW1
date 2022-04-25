# BUG-10

## Category

- [10] Wrong Operator

## Description

In this code, assignment operator `=` is need, instead of Equality operator `==`.


## Affected Lines in the original program

In `circle.c:61` and `circle.c:84`.

```c
// line 61
y == round(center_y -
               sqrt(radius * radius - (x - center_x) * (x - center_x)));

// line 84
x == round(center_x -
           sqrt(radius * radius - (y - center_y) * (y - center_y)));
```

## Expected vs Observed

When the program is executed with proper arguments, it is expected to work properly. That means proper circular line should created on the image. However, we observed some missing points on the circular line.

## Steps to Reproduce

### Command

```bash
./circle test_imgs/desert.png output.png 75 75 50 123456
```

### Proof-of-Concept Input (if needed)

(attached: poc.png)

## Suggested Fix Description

We can solve this bug by modifying `==` -> `=`.