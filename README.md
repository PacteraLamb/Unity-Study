# 如何实现平稳过渡？
可以考虑使用Time.deltaTime实现  有待考证

# 一些行业案例

# VR看车

## 3D Cat 主要是做云渲染 https://www.3dcat.live/demo.html   
  1. 实现demo1 https://app.3dcat.live/share-app?appName=ASTON&appKey=x1jANFViE42JDbjR&official=true 
 
# 一些实用库
## Dotween 一个很实用的动画库
  - 移动物体 DOLocalMove?()

# 如何解决切换视角进入车内产生的穿透现象
做两个相机渲染  然后到门时切换渲染，


# Unity-UI Toolkit. &&  UGUI
# Unity UI Toolkit。  个人感觉目前还不够完善，使用起来还不如UGUI灵活
## 1.从 Package Manager 安装 UI 工具包软件包：
  - 1.单击 Add (+) 
  - 2.从菜单中选择 Add package from git URL… 
  - 3.在文本字段中，输入 com.unity.ui 
  - 4.单击 Add。
  
## 2.安装UI Builder
   - 通过修改项目下-->Packages-->manifest.json 方式安装
      - 添加 "com.unity.ui.builder": "1.0.0-preview.18"
         - 关于版本的问题我的理解是要和UIToolkit对应起来，如果出现错误unity会提示你修改的。
   - 应该有其他安装方式,暂时没有过多关注.
   - 官方安装方式 https://docs.unity3d.com/Packages/com.unity.ui.builder@1.0/manual/index.html
   
## 3.编写一个Hello world!
   1. 创建一个空的GameObject
      - Hierarchy 下右键 --> Create Empty
   2. 为GameObject添加UI Document、Input System Event System(UI ToolKit)组件
      - 选中刚刚创建的GameObject 
      - Inspector面板 单击 Add Component
      - 添加相应的组件
   3. 为刚刚创建的GameObject添加 Panel 和 Source
       - Project-->Assets下新建UI文件夹（可选）
       - 在第一步创建的文件夹下创建 Panel Settings Asset
            - 具体步骤 Create --> UI Toolkit --> Panel Settings Asset
       - 在第一步创建的文件夹下创建 Source
            - 具体步骤 Create --> UI Toolkit --> UI Document
       - 将 创建的Panel和Source文件连接到创建的GameObject
        - 选中GameObject
        - 将创建的Panel拖动到 GameObject下UI Document下的PanelSettings
        - 将创建的Source拖动到 GameObject下UI Document下的Source Asset
   4. 编写UI
      - 选中第三步创建的Source(UI Document) 右键Open 会弹出 UI BUilder面板
      - 将Controls(左下角)面板中的Label 拖动到Hierarchy面板
      - 选中Label 右侧Inspector面板 Label组下的Text输入Hello World！
      - 保存 回到unity的Game窗口 可以看到已经出现的我们刚才创建的组件
   5. 添加USS文件为组件自定义样式
      - 在第三步创建的UI文件夹下创建USS文件
        - 具体步骤 Create --> UI Toolkit --> Style Sheet
      - 编辑Source(第三步创建的UI Document)
        - 用文本编辑工具打开后在<ui:UXML ...></<ui:UXML>标签之间添加 <Style src="MyUI.uss" /> MyUI.uss为刚刚第一步创建的文件
      - 像写css一样写一个样式
        - 第一步创建的文件下添加
          ```css
            .MyUI{
              color: red;
            }
          ``` 
       - 将刚刚创建的样式添加到Source
        参考第四步的 编写UI 找到Style Class List输入刚才书写的MyUI 单击Add Style Class to List
       - 保存 回到unity的Game窗口 可以看到已我们刚才创建的组件 文字已经变成红色了
  ## 4.一些与CSS不太相同的样式属性
    ```
      文字水平居中 -unity-text-align: upper-center;
      文字水平垂直居中 -unity-text-align: middle-center;
      文字加粗 -unity-font-style: bold;
    ```
   
# UGUI

##如何让按钮之类的提示信息跟随模型，而不是固定在屏幕上
  - 如果是UI需要先将Canvas的渲染模式改成World Space 然后将UI放到模型之下即可,此时的模型就相当于一个模型物体
    - 更改渲染模式选中要更改的UI右侧<b>Inspector</b>--><b>Canvas</b>组件--><b>Render Mode</b>

## 当使用Canvas Group（只作用于UI）模拟点击的显示与隐藏时，可能会因为图层顺序原因导致无法点击。
  - 解决办法。在外层套一个空的GameObject，通过SetActive来控制物体的显示与隐藏

## 如何将Canvas导出复用
  - 将Canvas做成预制体
  1. 新建Perfabs文件夹
  2. 将要导出的Canvas拖入Perfabs
  3. 右键导出
 
## Button按钮可视化实现--> 按钮点击更换按钮的背景
  1. 将Inspector面板下的Button组件的<b>Transition</b>设置成<b>Sprite Swap</b>
  2. 将Transition属性下的<b>Selected Sprite</b>属性设置成想要更换的背景即可
  
  
# Unity中一些脚本的笔记

## 1.通过实现IPointerClickHandler接口来实现点击事件 只作用于UI,  3d物体使用OnMouseDown来实现
直接挂到物体上即可实现点击，不需要其它的指定
```c#
public class ChangeShader : MonoBehaviour,IPointerClickHandler
{
    void Start()
    {
    }

    // Update is called once per frame
    void Update()
    {
        
    }
    public void OnPointerClick(PointerEventData eventData)
    {
      //业务处理  
    }
}
```

## 2.关于 Color类的事项
当使用RGB值时要/255f 才能的到相应的值,支持RGBA
```c#
  new Color(68 / 255f, 138 / 255f, 255 / 255f))
```

## 3.关于使用Resources加载本地模型的问题
### 加载的模型可能会位于（0，0，0）坐标，如果此时相机的坐标也是0，0，0难么可能会导致无法看到加载的物体，此时需要动态的设置一下加载的物体的坐标以达到想要的效果
```c#
  //把资源加载到内存中
  Object cubePreb = Resources.Load("Prefabs/Cube", typeof(GameObject));
  //用加载得到的资源对象，实例化游戏对象，实现游戏物体的动态加载
  GameObject cube = Instantiate(cubePreb) as GameObject;
  cube.transform.position = new Vector3(0,0,10);
 ```
 
## 4.关于unity的打包AssetBundles和加载问题
AssetBundles官方文档 --> https://docs.unity3d.com/Manual/AssetBundles-Workflow.html

###  打包
1.构建 AssetBundles
  在 Assets 文件夹中创建一个名为 Editor 的文件夹，并在该文件夹中放置一个包含以下内容的脚本：
  ```c#
  using UnityEditor;
  using System.IO;

  public class CreateAssetBundles
  {
      //
      [MenuItem("Assets/Build AssetBundles")]
      static void BuildAllAssetBundles()
      {
          string assetBundleDirectory = "Assets/AssetBundles";
          if(!Directory.Exists(assetBundleDirectory))
          {
              Directory.CreateDirectory(assetBundleDirectory);
          }
          BuildPipeline.BuildAssetBundles(assetBundleDirectory, 
                                          BuildAssetBundleOptions.None, 
                                          BuildTarget.StandaloneWindows);
      }
  }
```
  该脚本在 Assets 菜单底部创建一个名为Build AssetBundles的菜单项，用于执行与该标签关联的函数中的代码。当您单击Build AssetBundles 时，会出现一个带有构建对话框的进度条。这将获取您用 AssetBundle 名称标记的所有资产，并将它们放置在路径assetBundleDirectory定义的文件夹中。
  
  2.本地加载 AssetBundles 和 Assets
  从本地存储加载，<strong>AssetBundles.LoadFromFile</strong>API
  ```c#
    public class LoadFromFileExample : MonoBehaviour {
      void Start() {
          //Combine拼接方法 参数一为步骤1中设置的路径 参数二（car-911）为打包的ab包的名字
          var myLoadedAssetBundle = AssetBundle.LoadFromFile(Path.Combine("Assets/AssetBundles/","car-911"));
          if (myLoadedAssetBundle == null)
          {
              Debug.Log("Failed to load AssetBundle!");
              return;
          }
          //此处的car-911为模型名字
          var prefab = myLoadedAssetBundle.LoadAsset<GameObject>("car-911");
          //加载模型
          Instantiate(prefab);
          //因为Instantiate(prefab) 默认将模型加载到0，0，0坐标位置，如果要设置坐标可以参考下列的加载方法
          GameObject car_911 =  Instantiate(prefab) as GameObject;
          car_911.transform.position = new Vector3(0,0,15);
      }
    }
  ```
  
  3.自己托管AB包  结合UnityWebRequest实现动态加载
  ```c#
    IEnumerator InstantiateObject()
    {
        //托管的AB包为打包出来的两个文件（.manifest 和 另一个无后缀文件）中的无后缀文件
        string url = "要加载的AB包的路径";
        UnityWebRequest www = UnityWebRequestAssetBundle.GetAssetBundle(url, 0); ;
        yield return www.SendWebRequest(); ;
        if (www.result != UnityWebRequest.Result.Success)
        {
            Debug.Log(www.error);
        }
        else
        {
            //加载的模型名为为.manifest中的定义的模型名字而不是AB包的名字
            AssetBundle bundle = DownloadHandlerAssetBundle.GetContent(www);
            GameObject prefab = bundle.LoadAsset<GameObject>("car-911");
            GameObject car_911 = Instantiate(prefab) as GameObject;
            car_911.transform.position = new Vector3(0, 0, 15);
        }
    }
  ```
  
  ## 模型添加点击事件
  ### 添加Mesh Collider组件 或者Box Collider等碰撞体
  不同组件的效率不同
  
  ## 如何让模型拥有透明效果
  ### 只需更改材质（Material）的渲染模式为（Rendering Mode）为Fade模式 然后再调整颜色的透明度即可
  
  ## 模型更改旋转的中心点方法
  ### 只需要给要旋转的物体添加一个空的Object组件然后调整父组件的位置即可。 
   ~ 例如 将车门的中心点 从中间改为左侧只需要将一个空的物体拖动至车门的左侧，然后将车门模型放入这个空物体即可
   
  ## 实现鼠标右键左右滑动控制A围绕B旋转
  targetObject --> A
  centerObject --> B
  ```c#
    if (Input.GetMouseButton(1)) { 
        targetObject.transform.RotateAround(
            centerObject.transform.position,
            Vector3.up,
            Input.GetAxis("Mouse X") * speed
            );
    }
  ```
  
 ## 当使用GameObject.Find获取物体时可能出现的空指针异常
 ###
 当我们使用GameObject.Find获取一个物体时可能会报错 
  unity NullReferenceException: Object reference not set to an instance of an object
  - 原因1：指定名称时没有加前缀的路径
       - 例如 UI/ChangePlane/ColorView  如果我们只写ColorView则会报错
 # 保持物体和相机的角度不变，参考此处的代码（可以套用到任意两个物体）
 ```c#
  //保持摄像机和目标物体的角度不变
  //x + y = z
  Quaternion temp = Quaternion.Euler(
          Target.transform.rotation.eulerAngles
          +
          mycamera.transform.rotation.eulerAngles
      );
  Target.transform.rotation = Quaternion.Euler(
      temp.eulerAngles
      -
      Target.transform.rotation.eulerAngles 
      );
  ```
  # 延迟执行
  
```c#
using System.Collections;
using UnityEngine;
using System;
public class Pactera_Delay : MonoBehaviour
{
    public static IEnumerator DelayToInvoke(Action action, float delaySeconds)
    {
        yield return new WaitForSeconds(delaySeconds);
        action();
    }

    /* 调用
     * StartCoroutine(Pactera_Delay.DelayToInvoke(() => {
                }, 1f));
     */
}
```


