## 配置
0. [下载 JavaFX - Gluon](https://gluonhq.com/products/javafx/)
1. 新建项目
2. 添加 JavaFX 库
	- InteliJ IDEA
	- 文件 (Files)
	- 项目结构 (Program Settings)
	- 库 (Libraries)
	- +
	- 选择 `%javafx-sdk-<version>\lib%` 目录下的全部 `.jar`文件
![[Pasted image 20241114065733.png]]![[Pasted image 20241114065834.png]]
3. 配置 VM(Java Virtual Machine, Java 虚拟机) 选项
	- 运行 - 更多操作
	- 使用形参运行...
	- 修改选项
	- 添加虚拟机选项
	- 在VM选项中输入
		`--module-path <%javafx-sdk-<version>\lib% (JavaFX SDK 库的路径)> --add-modules javafx.controls,javafx.fxml`

		> 这里的 `--module-path` 指定了 JavaFX 的库路径，`--add-modules` 加载了 `javafx.controls` 和 `javafx.fxml` 模块，这些模块包含了基本的 JavaFX 控件和布局支持

	- 应用
	![[Pasted image 20241114070708.png]]
	![[Pasted image 20241114070757.png]]
	![[Pasted image 20241114072453.png]]
或者在全局中设置:
- 运行/调试配置
- 编辑配置
- 编辑配置模板...
- 应用程序
- 修改选项
- 之后步骤后同上
![[Pasted image 20241114073211.png]]
![[Pasted image 20241114073244.png]]
![[Pasted image 20241114073359.png]]