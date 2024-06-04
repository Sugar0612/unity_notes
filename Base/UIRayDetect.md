### *Technical Summary*  
&emsp;
*To detect whether the mouse overlaps with an object on the screen, it is not necessary to obtain the screen coordinates and borders of the object to perform complex calculations. Unity provides us with **ray detection** and also provides a way to convert **mouse coordinates into rays**.*  

### Sample Code  
```cs
// Camera.main.ScreenPointToRay(Input.mousePosition)： Convert mouse coordinates to rays
// Physics.Raycast: X-ray Detection
if (Physics.Raycast(Camera.main.ScreenPointToRay(Input.mousePosition), out hit))
{
    if (target_name == hit.collider.name)
    {
        // Do Something...
    }
}
```  

### Related Documents  
- [Physics.Raycast](https://docs.unity3d.com/cn/current/ScriptReference/Physics.Raycast.html)  
- [Unity 之 ScreenPointToRay()](https://blog.csdn.net/weixin_74850661/article/details/132404059)