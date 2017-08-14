#### Activity 生命周期
1.（打开First Activity）：经过onCreate、onStart、onResume后First Activity就展现啦；
2.（跳转至Second Activity）：首先First Activity暂停（onPause），
  接下来Second Activity展现（onCreate、onStart、onResume），最后First Activity停止（onStop）；
3.（返回到First Activity）：首先Second Activity暂停（onPause），
  接下来First Activity重新打开并展现（onRestart、onStart、onResume），最后Second Activity停止并销毁（onStop、onDestroy）；
4.（退出First Activity）：经过onPause、onStop、onDestroy后First Activity暂停、停止并最终销毁。
