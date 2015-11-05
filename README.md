# MP3CutAd
自动去掉MP3有声读物里面反复出现的广告

## 使用方法
1. 下载ffmpeg。代码里FFMpeg类中的path设置成ffmpeg的路径。
2. 运行这份代码，两个参数分别为：MP3文件所在的目录名、输出目录名。
3. 运行结束之后手动删除输出目录下的tmp子目录。

注意：输出目录需要留出足够的空间存临时文件，一小时的音频需要150M空间左右。

## 原理
找到**重复出现**的广告，然后去掉。

具体步骤如下：

1. 使用ffmpeg把MP3文件转成wav格式。（平均3.5秒一个文件）
2. 对wav文件做FFT。（大约2~3秒一个文件）
3. 对FFT的结果做LSH。（2、3合起来，平均10秒一个文件）
4. 两两对比，找到相似的片段。（大约0.5秒对比一组）

如果有50个文件，那么总时间大概是(3.5+10)*50 + 0.5*50*50 = 32分钟。


## TODO
* wav文件会占用大量磁盘空间，考虑直接对MP3做fft。
* 现在没有删除临时文件的功能。
* 目前是两两对比，找重复部分。考虑修改算法，归纳多处出现的广告，优化边界的识别。
* FFT+cos距离这种土办法是不是有高大上的替代方法？
* 边界判断土算法是不是有高大上的替代方法？



