# Beast Console

BeastConsole is evolution (hopefully) of SmartConsole,

该库主要服务于 `https://github.com/AlianBlank/GameFrameX` 作为子库使用。


# 使用方式(三种方式)
1. 直接在 `manifest.json` 文件中添加以下内容
   ```json
      {"com.pointcache.beastconsole": "https://github.com/AlianBlank/com.pointcache.beastconsole.git"}
    ```
2. 在Unity 的`Packages Manager` 中使用`Git URL` 的方式添加库,地址为：https://github.com/AlianBlank/com.pointcache.beastconsole.git

3. 直接下载仓库放置到Unity 项目的`Packages` 目录下。会自动加载识别

# 改动功能

1. 增加 `Packages` 的支持
2. 增加自定义类型列表的支持
3. 修改为必须手动调用初始化注册

# 以下为原内容

![License MIT](https://img.shields.io/badge/license-MIT-green.svg)

# Beast Console

![screen](https://i.imgur.com/HwZk4ZJ.jpg)


## Recently updated to remove any trace of UGUI. Now its pure IMGUI, with no additional clutter.

This project is possible because of the effort of amazing people at Cranium Software
this project is based of SmartConsole https://github.com/CraniumSoftware/SmartConsole

BeastConsole is evolution (hopefully) of SmartConsole,


# Console
* Backend is created by folks at CraniumSoftware.
* Use attributes to bind members 
* Register your own arbitrary commands/methods for any object(non monob as well) and provide parameters
* Autocomplete
* Both commands and variables support any number of subscribers, modify all objects at once.
* Multiline
* Suggestions
* History
* ConsoleUtility class containing methods to draw tables. (You can actually use ConsoleUtility pretty much by itself instead of Console class).

# Usage

setup:
	Drop Console prefab in scene, change parameters to your liking.
 
Attributes:

Console uses reflection to find attributes, to speed up the whole process we should mark any class that has uses console 
attributes with `[ConsoleParse]` attribute.

```csharp

[ConsoleParse]
public class AttributeTest : MonoBehaviour {

    [ConsoleVariable("testvar", "")]
    public float TestVariable = 5f;

    [ConsoleVariable("testproperty", "")]
    public bool TestPropertyVariable
    {
        set {
            Console.WriteLine("testproperty was set to: " + value);
        }
    }


    [ConsoleCommand("testMethod", "")]
	void TestMethod() {
        BeastConsole.Console.WriteLine("test method works");
    }

    [ConsoleCommand("testMethodWithParams", "")]
    public void TestMethodWithParams(float param1) {
        BeastConsole.Console.WriteLine("works :" + param1.ToString());

    }

    [ConsoleCommand("testMethodWith2Params", "")]
    public void TestMethodWith2Params(float param1, int param2) {
        BeastConsole.Console.WriteLine("works :" + (param1+ param2).ToString());

    }
}


```

Manual:

```csharp

public float Volume = 1f;
Console.RegisterVariable<float>("Volume", "", x => Volume = x, this);

Console.RegisterCommand("MoveUp", "", this, MoveUp);
   
private void MoveUp(string[] val) {
   transform.position += new Vector3(0, System.Convert.ToSingle(val[1]) , 0);
}

```
Manual method requires you to unregister commands and variables when done with an object.

See Example folder for more examples.

