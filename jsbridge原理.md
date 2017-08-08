#### javascript的哪些操作会被java捕获到？
* window.alert => onJSAlert
* window.confirm => onJSConfirm
* window.prompt => onJsPrompt
* window.location => shouldOverrideUrlLoading

#### 完整的jsbridge协议
```
jsbridge://className:callbackAddress/methodName?jsonObj
我们在js中调用native方法的时候，在js中注册一个callback，然后将该callback在指定的位置上缓存起来，然后native层执行完毕对应方法后通过WebView.loadUrl调用js中的方法，回调对应的callback。那么js怎么知道调用哪个callback呢？于是我们需要将callback的一个存储位置传递过去，那么就需要native层调用js中的方法的时候将存储位置回传给js，js再调用对应存储位置上的callback，进行回调
```

#### web前端调用native原理
```
利用js的iFrame（不显示）的src动态变化，触发java层webClient的shouldOverrideUrlLoading，然后让本地去调用javasript
```
#### 客户端调用js
```
webview.loadUrl("javascript:WebViewJavascriptBridge._handleMessageFromNative('%s');" );
```
