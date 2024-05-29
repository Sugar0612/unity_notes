### *Pitfalls*  
&emsp;
*I wrote a server using UnitySocket and used ScriptableObject as the database in order to achieve lightweight. However, I found in the later stages of development that the saved data would disappear when the UnityEditor layer was exited or the packaged exe file was exited, which was not what I wanted.*  

### Solution  
&emsp;
*In the UnityEditor layer, you can call the following code to save the corresponding resources when closing.*  
&emsp;
*But an error will be reported during the packaging process*  
&emsp;
*Related articles:*  &emsp;
* *[unity踩坑记录](https://blog.csdn.net/qq_37253520/article/details/120021205);*  
* *[Compile Error - The name 'EditorUtility' does not exist in the current context](https://forum.unity.com/threads/compile-error-the-name-editorutility-does-not-exist-in-the-current-context.680800/)*
```cs
EditorUtility.SetDirty(obj);
AssetDatabase.SaveAssets();
```  
&emsp;
*The correct way to handle this is to use Unity's own JsonUtility to serialize the data in ScriptableObject for persistent storage.*  
```cs
string json = JsonUtility.ToJson(obj);
File.WriteAllText(Application.persistentDataPath + "/Data.json", json);

if (File.Exists(Application.persistentDataPath + "/Data.json") && !Init)
{
    string jsonStr = File.ReadAllText(Application.persistentDataPath + "/Data.json");
    JsonUtility.FromJsonOverwrite(jsonStr, obj);
    Init = true;
}
```