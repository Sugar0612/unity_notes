- [*关于使用CancallationToken的标准*](https://github.com/Cysharp/UniTask#async-void-vs-async-unitaskvoid)
- [*想要用返回值还要使用Token的相关文章方法*](https://blog.csdn.net/weixin_44439733/article/details/135422739)

*正常写法Cancel()不会报错*
```cs
CancellationTokenSource m_cts = new CancellationTokenSource();
public async UniTaskVoid XXX()
{
    await UniTask.Yield(cancellationToken:m_cts.Token);
}

public UniTaskVoid cancel()
{
    m_cts.Cancel();
    m_cts.DisPlay();
    m_cts = new CancellationTokenSource();
}
```
*需要有返回值的写法。*
```cs
CancellationTokenSource m_cts = new CancellationTokenSource();
public async UniTask<T> XXX()
{
    T t;
    await UniTask.Yield(cancellationToken:m_cts.Token);
    return t;
}

public async void Invoke_async()
{
   T t = await XXX().SuppressCancellationThrow();
}

public UniTaskVoid cancel()
{
    m_cts.Cancel();
    m_cts.DisPlay();
    m_cts = new CancellationTokenSource();
}
```

*PS: 使用UniTaskVoid类型是不可await的~！*