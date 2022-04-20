# BUG-3

## Category

- Iteration errors

## Description

The method `filter_blur` should ignore the pixels of the square which fall outside the image. But in the original program, they are counted in the below loops and calculated the total number of pixels in square. 

```c
// filter.c:69
for (long y_offset = -radius; y_offset <= radius; y_offset++) {
  for (long x_offset = -radius; x_offset <= radius; x_offset++) { ... } }

// filter.c:86
int num_pixels = (2 * radius + 1) * (2 * radius + 1);
```

## Affected Lines in the original program

In range `filter.c:69` to `filter.c:86`.

## Expected vs Observed

The corner part of output image of filter blur should be calculated without pixels out of the original image, but it is observed that the boundary of image is ruined with transparent pixels, which is out of the image.  

## Steps to Reproduce

### Command

```bash
./filter poc.png out.png blur 50
```

### Proof-of-Concept Input (if needed)

(attached: poc.png)

## Suggested Fix Description

Set the iteration range to the inside of the original image size. And let the number of pixels out of bound exclude in the counting of blur area.  