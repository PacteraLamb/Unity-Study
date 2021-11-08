# Unity-UI Toolkit
Unity UI Toolkit
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
## 3.编写一个Hello world!
   - 1.创建一个空的GameObject
     - 1) Hierarchy 下右键 --> Create Empty
   - 2.为GameObject添加UI Document、Input System Event System(UI ToolKit)组件
     - 添加方法  
      - 选中刚刚创建的GameObject 
      - Inspector面板 单击 Add Component
      - 添加相应的组件
   - 3.为刚刚创建的GameObject添加 Panel 和 Source
     - 1) Project-->Assets下新建UI文件夹（可选）
     - 2) 在1)创建的文件夹下创建 Panel Settings Asset
          - 具体步骤 Create --> UI Toolkit --> Panel Settings Asset
     - 3) 在1)创建的文件夹下创建 Source
          - 具体步骤 Create --> UI Toolkit --> UI Document
     - 4) 将 2),3)的文件连接到创建的GameObject
      - 选中GameObject
      - 将2)创建的Panel拖动到 GameObject下UI Document下的PanelSettings
      - 将3)创建的Source拖动到 GameObject下UI Document下的Source Asset
    - 4.编写UI
      - 1) 选中3-->3)创建的UI Document 右键Open 会弹出 UI BUilder面板
      - 2) 将Controls(左下角)面板中的Label 拖动到Hierarchy面板
      - 3) 选中Label 右侧Inspector面板 Label组下的Text输入Hello World！
      - 4) 保存 回到unity的Game窗口 可以看到已经出现的我们刚才创建的组件
    - 5.添加USS文件为组件自定义样式
      - 1) 在第三步创建的UI文件夹下创建USS文件
        - 具体步骤 Create --> UI Toolkit --> Style Sheet
      - 2) 编辑Source(第三步创建的UI Document)
        - 用文本编辑工具打开后在<ui:UXML ...></<ui:UXML>标签之间添加 <Style src="MyUI.uss" /> MyUI.uss为刚刚第一步创建的文件
      - 3) 像写css一样写一个样式
        - 第一步创建的文件下添加
          ```css
            .MyUI{
              color: red;
              display: flex;
              justify-content: center;
            }
          ``` 
  
