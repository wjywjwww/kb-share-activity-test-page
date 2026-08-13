# KBBannerWebController shareActivity Test Page

This is a static GitHub Pages test page for `KBBannerWebController`.

The share button builds this payload:

```js
[
  "shareActivity",
  shareURL,
  title,
  imageURL,
  description,
  scene
]
```

The page supports multiple native bridge styles.

iOS WKWebView:

```js
window.webkit.messageHandlers.postAction.postMessage(payload)
```

Android WebView array-argument style:

```js
window.Android.postAction([
  "shareActivity",
  shareURL,
  title,
  imageURL,
  description,
  scene
])
```

HarmonyOS array-argument style:

```js
(window.HarmonyOS || window.Harmony || window.harmonyOS || window.harmony).postAction(data)
```

Android JSON style:

```js
window.Android.postAction(JSON.stringify(payload))
window.NativeBridge.postAction(JSON.stringify(payload))
window.postAction.postMessage(JSON.stringify(payload))
```

The page has a bridge mode selector:

- Auto
- iOS
- Android array
- Android multi-argument fallback
- Android JSON
- HarmonyOS

The dedicated Android button always calls:

```js
window.Android.postAction(data)
```

The dedicated HarmonyOS button always calls:

```js
(window.HarmonyOS || window.Harmony || window.harmonyOS || window.harmony).postAction(data)
```

`vConsole` is enabled on the page so Android and iOS WebView logs are visible on device.

iOS parameter order matches the current Swift implementation:

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

After native share succeeds, call this page method to update the UI:

```swift
webView.evaluateJavaScript("window.shareActivityCallback()")
```

The canonical callback is:

```js
window.shareActivityCallback()
```

The page also exposes these compatible success aliases:

- `window.onShareActivityResult()`
- `window.nativeShareActivityCallback()`
- `window.KBBannerWebController.shareActivityCallback()`
