[](id:step1)
## Step 1. Unzip the demo project

1. Download the [TRTC demo](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.115.vcube/TRTC-API-Example.zip) which has integrated Tencent Effect SDK.
2. Import the xMagic module from the demo into your actual project.

[](id:step2)

## Step 2. Open the `build.gradle` of the app module
1. Replace the `applicationId` with the package name under the obtained trial license.
2. Add the `gson` dependency settings.
```groovy
configurations{
	all*.exclude group:'com.google.code.gson'
}
```

[](id:step3)
## Step 3. Integrate the SDK API
You can refer to the `ThirdBeautyActivity` class of the demo.
1. **Authorize:**
```java
  // For authentication precautions and error codes, see https://cloud.tencent.com/document/product/616/65891#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83
XMagicImpl.checkAuth((errorCode, msg) -> {
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    showLoadResourceView();
                } else {
                    TXCLog.e(TAG, "Authentication failed. Check the authentication URL and key" + errorCode + " " + msg);
                }
            });
```
2. **Initialize the material:**
```java
private void showLoadResourceView() {
        if (XmagicLoadAssetsView.isCopyedRes) {
            XmagicResParser.parseRes(getApplicationContext());
            initXMagic();
        } else {
            loadAssetsView = new XmagicLoadAssetsView(this);
            loadAssetsView.setOnAssetsLoadFinishListener(() -> {
                XmagicResParser.parseRes(getApplicationContext());
                initXMagic();
            });
        }
    }
```
3. **Enable push settings:**
```java
mTRTCCloud.setLocalVideoProcessListener(TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE, new TRTCCloudListener.TRTCVideoFrameListener() {
    @Override
    public void onGLContextCreated() {
    }
    @Override
    public int onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame) {
    }
    @Override
    public void onGLContextDestory() {
    }
});
```
4. **Pass the `textureId` into the SDK for rendering:**
In the `onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame)` method of the `TRTCVideoFrameListener` API, add the following code: 
```
dstFrame.texture.textureId = mXMagic.process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
```
5. **Pause/Terminate the SDK**:
`onPause()` is used to pause the beauty filter effect, which can be executed in the `Activity/Fragment` lifecycle method. The `onDestroy` method needs to be called in the GL thread (the `onDestroy()` of the `XMagicImpl` object can be called in the `onTextureDestroyed` method). For more information, see the demo.
```java
mXMagic.onPause();   // Pause, which is bound to the `onPause` method of `Activity`
mXMagic.onDestroy();  // Terminate, which needs to be called in the GL thread
```
6. **Add the SDK beauty filter panel to the layout:**
```xml
    <RelativeLayout
        android:layout_above="@+id/ll_edit_info"
        android:id="@+id/livepusher_bp_beauty_pannel"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
```
7. **Initialize the panel:**
```java
      private void initXMagic() {
          if (mXMagic == null) {
              mXMagic = new XMagicImpl(this, mBeautyPanelView);
          }else {
              mXMagic.onResume();
          }
      }
```

    See the `ThirdBeautyActivity.initXMagic();` method of the demo for details.

