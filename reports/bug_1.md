# BUG-1

## Category

- Local persisting pointers

## Description

The pointer of struct pixel `*neg` is return value of function `get_pixel()`, which is address of local variable `px` in function `get_pixel()`. 

Because the variable `px` is free when the function `get_pixel()` returned, the pointer `*neg` becomes null pointer. So the `Segmentation fault` is occured, when the pointer `neg` tries to access any properties of struct pixel. (Ex, `neg->red`). 

## Affected Lines in the original program

In range `filter.c:127` to `filter.c:135`

## Expected vs Observed

We expect that the pointer `neg` points a new pixel struct, but it is observed as null pointer. So, we also observed a segmentation fault, when the pointer `neg` tries to access property of struct `pixel`. (Ex. `neg->red`)

## Steps to Reproduce

### Command

```
./filter poc.png out.png negative
```

### Proof-of-Concept Input (if needed)

(attached: poc.png)

## Suggested Fix Description

Declare struct pixel `neg` directly, instead of using function `get_pixel()`. This allows the variable `neg` to be a struct of pixel, not null pointer. And becasue using struct instead of pointer of struct, modify `->` into `.`.