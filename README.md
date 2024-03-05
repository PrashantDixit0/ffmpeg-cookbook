# CLI Commands

### Cut/Trim Video
`-ss` specifies the starting position and `-t` specifies the duration from the start position

`-c:v copy -c:a` copy commands copy the original audio and video without re-encoding.

```bash
ffmpeg -i input.mp4 -ss 00:00:00 -t 00:00:35 -c:v copy -c:a copy output.mp4
```

`-to` to specify an exact time to cut to from the starting position

```bash
ffmpeg -i input.mp4 -ss 00:00:00 -to 00:00:30 -c:v copy -c:a copy output.mp4
```

### Compress Video
Push the compression level further by increasing the CRF value — add, say, 4 or 6, since a reasonable range for H.265 may be 24 to 30. 

```bash
ffmpeg -i input.mp4 -vcodec libx265 -crf 28 output.mp4
```

### GIF converter

following skip the first 10 seconds `-ss 10` of the input and create a 5 second output `-t 3`

Change as per your need
```bash
ffmpeg -i input.mp4 -vf "fps=5,scale=640:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif
```

### Resize GIFs
change scale for relatively resizing gifs
```bash
ffmpeg -i input.gif -vf "scale=iw*3/4:ih*3/4" resized_ot.gif
```