# KBBannerWebController shareActivity Test Page

This is a static GitHub Pages test page for `KBBannerWebController`.

The share button calls:

```js
window.webkit.messageHandlers.postAction.postMessage([
  "shareActivity",
  shareURL,
  title,
  imageURL,
  description,
  scene
]);
```

Parameter order matches the current Swift implementation:

```swift
let shareURL = bodys[1]
let title = bodys[2]
let imageURL = bodys[3]
let shareDescription = bodys[4]
let scene: WXScene = bodys[5] == "1" ? WXSceneTimeline : WXSceneSession
```

Scene values:

- `"0"`: WeChat session
- `"1"`: WeChat timeline

After native share finishes, call one of these page methods to update the UI:

```swift
webView.evaluateJavaScript("window.shareActivityCallback({success:true,message:'分享成功'})")
webView.evaluateJavaScript("window.shareActivitySuccess({success:true,message:'分享成功'})")
webView.evaluateJavaScript("window.shareActivityFail({success:false,message:'分享失败或取消'})")
```

The canonical callback is:

```js
window.shareActivityCallback(result)
```

The page also exposes these compatible aliases:

- `window.shareActivitySuccess(result)`
- `window.shareActivityFail(result)`
- `window.onShareActivityResult(result)`
- `window.onShareActivitySuccess(result)`
- `window.onShareActivityFail(result)`
- `window.nativeShareActivityCallback(result)`
- `window.KBBannerWebController.shareActivityCallback(result)`

