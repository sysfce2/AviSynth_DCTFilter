## DCTFilter
	This plugin is a rewrite of DctFilter for avisynth.

### Version:
	0.5.1

### Requirement:
	- Windows Vista sp2 or later
	- SSE2 capable CPU
	- Avisynth 2.60 / Avisynth+MT r2085 or later
	- Microsoft VisualC++ Redistributable Package 2019.

### Usage:
```
DCTFilter8(clip, float, float, float, float, float, float, float, float,
		 float "x40", float "x41", float "x42", float "x43", int "chroma", int "opt")
```
Execute 8x8 DCT to image.

	clip: All planar formats(8/10/12/14/16bit and float, YUV/RGB with/without alpha) are supported.

	float: All of which must be specified as in the range (0.0 <= x <= 1.0).
		These correspond to scaling factors for the 8 rows and columns of the 8x8 DCT blocks.
		The leftmost parameter corresponds to the top row, left column.
		This would be the DC component of the transform and should always be left as 1.0.

	x40, x41, x42, x43: 0.0 <= x <= 1.0, default=1.0
		if planes's width and/or plane's height is not mod 8 but mod 4, DCTFilter8 execute 4x4 DCT
		to the most right/bottom 4 columns/rows.
		These correspond to scaling factors for the 4 rows and columns of the 4x4 DCT blocks.
		The leftmost parameter corresponds to the top row, left column.

	chroma:	0 = copy from source (on RGB, B and R planes are copied).
			1 = process (default)
			2 = do not process nor copy, output will be trash.
			note: alpha will be copied anytime. 

	opt: Specify which CPU optimization are used.
		0 = use c++ routine.
		1 = use SSE2 + SSE routine if possible. when SSE2 can't be used, fallback to 0.
		2 = use SSE4.1 + SSE2 + SSE routine if possible. when SSE4.1 can't be used, fallback to 1.
		others = use AVX2 + FMA3 + AVX routine if possible. WHen AVX2 can't be used, fallback to 2.(default)

	Note: the first 9 parameters are unnamed and do not have a default so they must be specified.

```
DCTFilter8D(clip, int diagonals_count, int "x4", int "chroma", int "opt")
```
	clip: same as DCTFilter8.

	diagonasl_count: must be an integer from 1-14 saying how many of these diagonals must be zeroed, starting from the lower right hand corner.

	x4: diagonals count for 4x4DCT.
		 1 <= x <= 6, default=1

	chroma: same as DCTFilter.

	opt: same as DCTFilter.

```
DCTFilter4(clip, float, float, float, float, int "chroma", int "opt")
```
Execute 4x4 DCT to image.

	clip: same as DCTFilter8.

	float: All of which must be specified as in the range (0.0 <= x <= 1.0).
		These correspond to scaling factors for the 4 rows and columns of the 4x4 DCT blocks.
		The leftmost parameter corresponds to the top row, left column.
		This would be the DC component of the transform and should always be left as 1.0.

	chroma:	same as DCTFilter8.

	opt: same as DCTFilter8.

	Note: the first 5 parameters are unnamed and do not have a default so they must be specified.

```
DCTFilter4D(clip, int diagonals_count, int "chroma", int "opt")
```
	clip: same as DCTFilter8.

	diagonasl_count: must be an integer from 1-6 saying how many of these diagonals must be zeroed, starting from the lower right hand corner.

	chroma: same as DCTFilter.

	opt: same as DCTFilter.

```
DCTFilter(clip, float, float, float, float, float, float, float, float,
		 float "x40", float "x41", float "x42", float "x43", int "chroma", int "opt")
```
```
DCTFilterD(clip, int diagonals_count, int "x4", int "chroma", int "opt")
```
	These 2 filters are just aliases of DCTFilter8 and DCTFilter8D for backward compatibility.


### License:
Copyright (c) 2016, OKA Motofumi <chikuzen.mo at gmail dot com>

Permission to use, copy, modify, and/or distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH
REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND
FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT,
INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM
LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR
OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
PERFORMANCE OF THIS SOFTWARE.

### Source code:
	https://github.com/chikuzen/DCTFilter
