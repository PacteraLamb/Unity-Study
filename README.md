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
     - 2) 在第一步创建的文件夹下创建 Panel Settings Asset
          - 具体步骤 Create --> UI Toolkit --> Panel Settings Asset
     - 3) 在第一步创建的文件夹下创建 Source
          - 具体步骤 Create --> UI Toolkit --> UI Document
     - 4) 将 2),3)的文件连接到创建的GameObject
