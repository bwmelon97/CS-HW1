# BUG-12

## Category

- [5] Heap Overflow

## Description

In the case that `square_width` is bigger than `width` or `height` of image, and the case that `width` or `height` are not divided with `square_width`, `image_data[square_top_left_y + y][square_top_left_x + x]` accesses the area that is not allocated for itself. (which means overflow in heap)


## Affected Lines in the original program

In `checkerboard.c:113` and `checkerboard.c:114`.

```c
for (int x = 0; x < square_width; x++) {
    for (int y = 0; y < square_width; y++) { ... }
}
```

## Expected vs Observed

In the case that `square_width` is bigger than `width` or `height` of image, and the case that `width` or `height` are not divided with `square_width`, We expected that squares of rightmost and bottom becomes rectangle but the program doesn't crash. But we observed an error due to heap overflow.

```bash
malloc(): corrupted top size
Aborted (core dumped)
```

## Steps to Reproduce

### Command

```bash
./checkerboard output.png 100 100 200 123456 654321
./checkerboard output.png 300 300 200 123456 654321
```

## Suggested Fix Description

Check the condition` square_top_left_x + x < width` and `square_top_left_y + y < height` in the for loop.

```c
for (int x = 0; square_top_left_x + x < width && x < square_width; x++) {
    for (int y = 0; square_top_left_y + y < height && y < square_width; y++) { ... }
}
```

