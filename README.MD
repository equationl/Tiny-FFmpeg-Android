# Tiny-FFmpeg-Android
![](https://api.bintray.com/packages/likehide/maven/tiny-android-ffmpeg/images/download.svg)

This is a tiny FFmpeg project fork from  [formatBCE](https://github.com/formatBCE/FFmpeg-Android).
Execute FFmpeg commands with ease in your Android project.

[中文说明](./README_ZH.md)

## Note
It will be get **Permission denied** error in targetSdkVersion 29(Android 10)

## Features
- Smaller package, only 21kb in size
- Support for most CPU architectures (including 64-bit)
-- armv7
-- armv7-neon
-- armv8
-- x86
-- x86_64
-- arm64-v8a
- The developer or user can choose to download the binary suitable for their device.
- Because the library itself does not contain binaries, you can bypass 64-bit detection on Google Play.

## Usage
### Getting Started
Include the dependency
```gradle 
implementation 'com.equationl.ffmpeg:tiny-android-ffmpeg:1.1.8'
```
_Replace the 1.1.8 to latest version_
### Start using
#### 1.Get Rady

Remember to check if the device is supported before use and if the binary exists and is available.
1.Check for support：
```java 
ffmpeg.isSupported()
``` 
2.Check if binary file exist
```java 
ffmpeg.isFFmpegExist()
``` 
3.If not exist, you need download by yourself

**You can get all ffmpeg binary file at [here](https://github.com/formatBCE/FFmpeg-Android/tree/master/android-ffmpeg/src/main/assets), 
Please download these files and upload them to your own server, and then implement the download files in your project.**

4.Apply the download file to project
```java 
ffmpeg.setFFmpegFile(file);
``` 
5.The callback of apply file
```java 
ffmpeg.setFFcheckFileListener(new FFcheckFileListener() {
            @Override
            public void onCopyFileFail(IOException e) {
                Log.e(e);
            }

            @Override
            public void onAllFinish() {

            }

            @Override
            public void onVerifyFileFail() {
                Log.e("check file fail!");
            }
        });
``` 

#### 2.Using
In this sample code we will run the ffmpeg -version command.
```java
FFmpeg ffmpeg = FFmpeg.getInstance(context);
  // to execute "ffmpeg -version" command you just need to input "-version"
String[] cmd = {"-version"};
ffmpeg.execute(cmd, new ExecuteBinaryResponseHandler() {

    @Override
    public void onStart() {}

    @Override
    public void onProgress(String message) {}

    @Override
    public void onFailure(String message) {}

    @Override
    public void onSuccess(String message) {}

    @Override
    public void onFinish() {}

});
```

Stop (or Quit) the FFmpeg process
If you want to stop the running FFmpeg process, simply call `.sendQuitSignal()` on the `FFtask` that is running:

```java
FFmpeg ffmpeg = FFmpeg.getInstance(context);
FFtask ffTask = ffmpeg.execute( ... )

ffTask.sendQuitSignal();
```

_NOTE: This will result in `onFailure` being called instead of `onSuccess`._



#### 3.Sample
Please check [demo](https://github.com/equationl/Tiny-FFmpeg-Android/tree/master/sample/src/main/java/com/equationl/ffmpeg/example/MainActivity.java)

## Thanks
This project fork from [formatBCE](https://github.com/formatBCE/FFmpeg-Android)

formatBCE fork from [bravobit](https://github.com/bravobit/FFmpeg-Android)

bravobit fork from[WritingMinds](https://github.com/WritingMinds/ffmpeg-android-java)

