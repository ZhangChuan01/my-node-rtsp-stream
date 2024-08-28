my-node-rtsp-stream
================
此项目基于node-rtsp-stream进行一些改造，增加一些对异常情况的监听，主要是个人项目使用

1. 10秒没有视频流 emit 'novideo'
2. 视频流异常 emit 'exit'
3. 视频流ws连接数量为0保持10秒  emit 'exit'

```
Stream = require('my-node-rtsp-stream')
stream = new Stream({
  name: 'name',
  streamUrl: 'rtsp://184.72.239.149/vod/mp4:BigBuckBunny_115k.mov',
  wsPort: 9999,
  ffmpegOptions: { // options ffmpeg flags
    '-stats': '', // an option with no neccessary value uses a blank string
    '-r': 30 // options with required values specify the value after the key
  }
})
stream.on('novideo', () => {console.log('无视频流')})
stream.on('exit', () => {console.log('视频流异常或ws连接数量为0')})
stream.on('exitWithError', () => {console.log('视频流异常')})
```