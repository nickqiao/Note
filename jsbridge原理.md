#### javascript的哪些操作会被java捕获到？
* window.alert => onJSAlert
* window.confirm => onJSConfirm
* window.prompt => onJsPrompt
* window.location => shouldOverrideUrlLoading

#### web前端调用native原理
```
利用js的iFrame（不显示）的src动态变化，触发java层webClient的shouldOverrideUrlLoading，然后让本地去调用javasript
```
