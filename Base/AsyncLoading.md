### *Asyn Loading*  
&emsp;
*SceneManager.LoadScene同步加载：进入的场景先进行资源的加载，待场景中所有的资源加载完成，才能进行场景和切换。并且原场景资源会立刻销毁。*  
&emsp;
*SceneManager.LoadSceneAsync() : 异步场景切换，Unity会在后台线程中加载所有资源，并保存之前场景的游戏对象，我们在加载过程中获取到加载的进度，可以播放一个真实的进度条，来看加载进度。*  
*实现一个场景异步加载场景，在加载期间显示加载画面*  

### Sample Code  
```cs
IEnumerator Load(string scene)
{
    AsyncOperation async = SceneManager.LoadSceneAsync(scene);
    async.allowSceneActivation = false; // 是否直接让async.progress等于1[不在后台加载]
    float progress = 0f;
    float realProgress = 0f;
    while (progress < 1f)
    {
        realProgress = async.progress;
        if (realProgress >= 0.9f)
            realProgress = 1f;
        if(realProgress > progress)
        {
            if (progress <= 0.9f)
                progress += Time.deltaTime;
            else
                progress += Time.deltaTime * 0.2f;
            progress = Mathf.Clamp(progress, 0f, 1f);
        }
        m_ProgressSlider.value = progress;
        yield return new WaitForEndOfFrame();
    }

    async.allowSceneActivation = true;
}
```  

### Related Documents  
- [Unity3d异步场景切换SceneManager.LoadSceneAsync之美](https://blog.csdn.net/weixin_44350205/article/details/99684904)  
- [SceneManager.LoadSceneAsync](https://docs.unity3d.com/cn/current/ScriptReference/SceneManagement.SceneManager.LoadSceneAsync.html)