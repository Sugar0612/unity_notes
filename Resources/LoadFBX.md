- 导入模型FBX

1. 文件结构尽量写成 xxx -> TEX 和 xxx.fbx 的形式, 方便查找。 
2. 如果需要更换贴图，可以在源文件 Materials->Location 下选择'Use External Materials(Legacy)'.

- 导入动画FBX

1. 动画如果需要自己添加 Animator, 发现怎么都无法将动画拖拽到 Motion上, 可以在源文件中找到 Rig->Animation Type 改成 'Generic'。
2. 如果发现播放动画组件和相机有轻微的偏移，可以在源文件的 Animation->Anim.Compression下改为 'Off', 或者将 Rotation Error, Position Error, Scale Error改为0.
3. 如果需要让一段完成的fbx动画分段播放，在源文件的Animation下的Clips，进行自己分段，然后在脚本中的 'Animation.Clips'中调用。
4. 将源文件中的Materials->Location修改为'Use External Materials(Legacy)', 可以修改fbx动画中的材质球。

- 关于优化

1. 模型fbx如果在动画fbx中也出现，在载入模型fbx时可以不用给他贴图，让他和动画fbx公用一套贴图, 这样可以减少打包的体积，提高加载速度，这一点在WebGL平台很明显。
2. 对FBX贴图优化，选择图片源文件，勾选'Generate Mip Maps', 把Default栏目下的'MaxSize'设置为 1024, 减少贴图的体积。
