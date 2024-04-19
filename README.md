# CLI Commands

### Cut/Trim Video
`-ss` specifies the starting position and `-t` specifies the duration from the start position

`-c:v copy -c:a` copy commands copy the original audio and video without re-encoding.

```bash
ffmpeg -i $input_file.mp4 -ss 00:00:00 -t 00:00:35 -c:v copy -c:a copy $output_file.mp4
```

`-to` to specify an exact time to cut to from the starting position

```bash
ffmpeg -i $input_file.mp4 -ss 00:00:00 -to 00:00:30 -c:v copy -c:a copy $output_file.mp4
```

### Compress Video
Push the compression level further by increasing the CRF value — add, say, 4 or 6, since a reasonable range for H.265 may be 24 to 30. 

```bash
ffmpeg -i $input_file.mp4 -vcodec libx265 -crf 28 $output_file.mp4
```

### GIF converter

following skip the first 10 seconds `-ss 10` of the input and create a 5 second output `-t 3`

Change as per your need
```bash
ffmpeg -i $input_file.mp4 -vf "fps=5,scale=640:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 $output_file.gif
```

### Resize GIFs
change scale for relatively resizing gifs
```bash
ffmpeg -i input.gif -vf "scale=iw*3/4:ih*3/4" $resized_output_file.gif
```

### Watermark
adjust watermark position

**center** - overlay=(main_w-overlay_w)/2:(main_h-overlay_h)/2 <br>
**top left** - overlay=(main_w-overlay_w):0<br>
**bottom left** - overlay=0:(main_h-overlay_h)<br>
**bottom right** - overlay=(main_w-overlay_w):(main_h-overlay_h)<br>

following command overlays watermark in right bottom
```bash
ffmpeg -i $input_file.mp4 -i /home/prashant/Downloads/icon.png -filter_complex "[1][0]scale2ref=oh*mdar:ih*0.1[logo][video];[video][logo]overlay=(main_w-overlay_w-20):(main_h-overlay_h-20)" $output_scaled.mp4
```

add oppacity in watermark <br>
`format=rgba,colorchannelmixer=aa=0.3`

```bash
ffmpeg -i $input_file.mp4 -i watermark.png -filter_complex "[1]format=rgba,colorchannelmixer=aa=0.3[logo];[logo][0]scale2ref=oh*mdar:ih[logo][video];[video][logo]overlay=overlay=(main_w-overlay_w-20):(main_h-overlay_h-20)" $output_center_cover_transparent.mp4
```

### Remove Audio From Video
You can remove audio by using the `-an` flag
```bash 
ffmpeg -i $input_file -c copy -an $output_file
```

### Add Audio to Video

```bash
ffmpeg -i $input_file.mp4 -i $input_file.mp3 -c copy -map 0:v:0 -map 1:a:0 $output_file.mp4
```