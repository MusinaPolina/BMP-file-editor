The application cuts a rectangle out of a BMP file with an image,
rotates this rectangle 90 degrees clockwise and saves the result to a separate
file.

All images (the original read and the saved result) are stored in the specified format:

* The general format is [BMP](https://en.wikipedia.org/wiki/BMP_file_format).
* The *DIB* format with header `BITMAPINFOHEADER` (version 3) is used within the BMP format.
* The value of the `biHeight` field (image height) is strictly greater than zero.
* 24 bits of color per pixel are used (one byte per color channel).
* Palette (color table) is not used.
* No compression is used.

### Console Application
The application is started with the following command:

```
./hw-01_bmp crop-rotate 'in-bmp' 'out-bmp' 'x' 'y' 'w' 'h'
```

Parameters used:

* `crop-rotate` - mandatory parameter indicating the action to be performed.
* `in-bmp` - name of the input file with the image.
* `out-bmp` - name of the output file with the image.
* `x`, `y` - coordinates of the upper left corner of the area to be cut and rotated.
  The coordinates start from zero, so *(0, 0)* is the upper left corner.
* `w`, `h` are, respectively, the width and height of the area before rotation.

Thus, if we denote the width and height of the original image by `W` and `H`, respectively,
the following inequalities are true for the correct arguments:

* `0 <= x < x + w <= W`
* `0 <= y < y + h <= H`.


In addition to the `crop-rotate` command, there are the `insert` and `extract` commands,
that allow you to hide a message inside the image
([steganography](https://en.wikipedia.org/wiki/Steganography)).
The `insert` command stores the message in the image and `extract` command extracts it from there.


### Encoding the message
The original message consists only of capital Latin letters, a space, a period, and a comma.

To send the message, in addition to the carrier image, you need a __key__ - a text file,
which describes in which pixels the bits of the message are encoded.
This file records on separate lines:

* The `x` and `y` coordinates (`0 <= x < W`, `0 <= y < H`) of the pixel in which the
  the corresponding bit.
* The letter `R`/`G`/`B` denotes the color channel in whose low-order bit the
  messages.

### Console application.
To save the secret line to an image, the application is started with the following command:
```
./hw-01_bmp insert 'in-bmp' 'out-bmp' 'key-txt' 'msg-txt'
```

To extract the secret string from the image, the application is started with the following command: ``:
```
./hw-01_bmp extract 'in-bmp' 'key-txt' 'msg-txt'
```

Parameters used:

* ``in-bmp`` - the name of the input file with the image.
* `out-bmp` - name of the output file with the image.
* `key-txt` - test file with a key.
* `msg-txt` - text file with a secret message.
