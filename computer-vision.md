# Computer Vision

Main filters for resizing: NEAREST, BILINEAR, BICUBIC, LANCZOS/ANTIALIAS

1. **Speed**: NEAREST &gt; BILINEAR &gt; BICUBIC &gt; LANCZOS/ANTIALIAS
2. **Output \(downscaling\) Quality**: LANCZOS/ANTIALIAS &gt; BICUBIC &gt; BILINEAR &gt; NEAREST
3. [**`Pillow` vs `cv2` resize**](https://github.com/python-pillow/Pillow/issues/2718): Pillow seems to come out better \(but really old discussion\). Also, the outputs \(resulting image pixel values\) are different!

Sources

* [https://pillow.readthedocs.io/en/3.0.x/releasenotes/2.7.0.html](https://pillow.readthedocs.io/en/3.0.x/releasenotes/2.7.0.html)
* [https://pillow.readthedocs.io/en/stable/handbook/concepts.html\#filters](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#filters)
* [https://stackoverflow.com/questions/7096323/python-pil-best-scaling-method-that-preserves-lines](https://stackoverflow.com/questions/7096323/python-pil-best-scaling-method-that-preserves-lines)

