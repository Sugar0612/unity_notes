### *DestroyImmediate*
*Destroy和DestroyImmediate都是Unity用于销毁游戏对象的方法。*  
*它们的语法是：*
```cs
Destroy(gameObject);
DestroyImmediate(gameObject);
```  
*都接受一个参数，即销毁的对象。*  

*但是它们是有一定区别的。*

*1） Destroy方法它会延迟销毁，当我们调用它时，不会立即销毁（但在同一帧内执行）；而DestroyImmediate方法在我们调用它时，会立即销毁对象。*

*2） DestroyImmediate是可以在编辑器脚本中使用，而Destroy不能在编辑器脚本中调用。*

*居于以上区别，使用时：*

*1）Destroy更适合在游戏运行状态对于一些临时对象进行动态销毁，或者在场景切换时把无用对象销毁；*  
*2）DestroyImmediate更适合在编辑器脚本状态下或者某些特定情况需要立即销毁对象的情境下调用，特别需要注意的时在调用DestroyImmediate方法销毁对象时，可能会打断正在进行的处理过程，所以我们对于DestroyImmediate要谨慎小心，确保调用时机得当。*  
### Related Documents   
- [Object.DestroyImmediate](https://docs.unity3d.com/cn/current/ScriptReference/Object.DestroyImmediate.html)  