# CLI Commands for Streaming IP Camera


### Stream RTSP stream to RTMP server

```bash 
ffmpeg -i rtsp://admin:password@192.168.1.1:554/ -c copy -f flv rtmp://rtmp.xyz.com:port/streamname
```

### Stream RTSP stream to RTMP server(if connection breaks pipeline after 30s)

```bash 
ffmpeg -rtsp_transport tcp -stimeout 30000000 -i rtsp://admin:bidaal2020@169.254.99.67:554/ -c copy -f flv rtmp://rtmp.bidaal.com:1935/lens/error
```