### 云点播支持上传哪些格式的媒体文件？

云点播支持上传格式如下：
- 视频：WMV、RM、MOV、MPEG、MP4、3GP、FLV、AVI、RMVB、TS、ASF、MPG、WEBM、MKV 、M3U8、WM、ASX、RAM、MPE、VOB、DAT、MP4V、M4V、F4V、MXF、QT、OGG。
- 音频：MP3、M4A、FLAC、OGG、WAV、RA、AAC、AMR。
- 封面图片：JPG、JPEG、PNG、GIF、BMP、TIFF、AI、CDR、EPS、TIF。

### 云点播上传文件有哪些方式，能否断点续传？
云点播上传文件的方式有：[控制台上传](https://intl.cloud.tencent.com/document/product/266/33890)、[服务端上传](https://intl.cloud.tencent.com/document/product/266/33912) 及 [客户端上传](https://intl.cloud.tencent.com/document/product/266/33921)。其中，客户端上传支持断点续传。

### 如何用控制台上传点播视频？
详细请参见 [上传视频](https://intl.cloud.tencent.com/document/product/266/33890)。


### 云点播上传如何获取上传进度？

目前不支持获取上传进度。

### 视频上传后，一般需要多长时间才能观看？
上传后的准备时间由视频时长和转码码率决定。

### 能否允许使用 App 或访问网页的客户自行上传视频？

云点播支持终端使用者直接上传文件，详细请参见 [客户端上传指引](https://intl.cloud.tencent.com/document/product/266/33921)。

### 云点播后台的上传区分目录是什么？
目前没有目录的功能，您可以通过分类的结构代表目录，将文件上传到对应的分类下，详细请参见 [修改视频分类](https://intl.cloud.tencent.com/document/product/266/33893)。

### 上传视频是否能压缩？
目前不支持压缩，仅只支持原视频上传。

### 如果有超大量视频文件，如何处理？
云点播会采用队列上传的方式保障视频文件的上传顺序。如果您有特别的需求，例如，TB 级甚至 PB 级超大容量的文件上传，请[提交工单](https://console.intl.cloud.tencent.com/workorder/category)。

### 上传返回 URL 为 HTTP，如何设置返回 HTTPS？
详细请参见 [默认分发配置](https://intl.cloud.tencent.com/document/product/266/35768)。

### 云点播 Web 端上传 SDK 对开发环境有哪些要求？
- 需要浏览器支持 HTML 5。
- 需要 App 服务器派发客户端上传签名，生成签名的方法请参见 [简单视频上传](https://intl.cloud.tencent.com/document/product/266/33924)。

### 云点播有哪些移动端上传 SDK?

目前，云点播为移动端提供了 Android 和 iOS 两种 SDK。
移动端 SDK 不仅提供了上传视频的 API，还针对用户的需求提供了丰富的视频编辑方面的 API，包括视频裁剪、拼接、滤镜及字幕等。

### 视频在上传签名时能否指定加密模板转码？
目前不支持，对应功能正在开发，后续会上线。

### 云点播视频上传接口是否支持 Go、PHP 及 .NET？
使用云 API3.0 的接口上传，3.0接口支持 Go SDK、PHP SDK 及 .NET SDK，详细请参见 [申请上传接口文档](https://intl.cloud.tencent.com/document/product/266/34120)。



### 视频上传成功后如何分享链接？
视频上传成功后分享链接步骤如下：
1. 控制台上申请发布。
2. 智能识别通过后，返回分享链接。
3. 使用该链接分享视频。

相关内容请参见 [视频发布](https://intl.cloud.tencent.com/document/product/266/33896)。

### 云点播上传的视频是否可以自动生成封面？

可以，云点播支持上传视频的时候，选取首帧作为封面或者拉取封面。


### 云点播视频拉取是否支持 M3U8 格式文件？

目前不支持拉取 M3U8 格式文件。
