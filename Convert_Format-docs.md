# CLI Commands to change media file from one to another

### Convert webp to mp4 format
```bash
ffmpeg -fflags +genpts -i input.webm -r 24 output.mp4
```
if convertion error comes like 
`[libx264 @ 0x560eb7c01840] width not divisible by 2 (wxh)`

then Try this
```bash
ffmpeg -fflags +genpts -i input.webm -vf "pad=ceil(iw/2)*2:ceil(ih/2)*2" -r 24 1.mp4
```

### Convert avi to mp4 format

```
ffmpeg -i input.avi -c:v copy -c:a copy output.mp4
```