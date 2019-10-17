目录
代码规范	2
1. 说明	2
2. 基本原则	2
3. C++与Python	2
4. 命名相关	2
5. 工程目录结构	3

Electron代码规范
1.	说明
Electron框架正如官网介绍是使用 JavaScript, HTML 和 CSS 构建跨平台的桌面应用的框架，框架分为前端和后端两个部分，根据前后端采用的技术不同分别遵循前后端所采用技术的代码规范
2.	基本原则
1)	不要直接在渲染进程操作主进程，通过进程通信的方式进行数据及事件响应
2)	nodejs请使用require方式引入资源不使用import方式引入
3)	多渲染进程传参请使用localStorage或sessionStorage
4)	资源下载不下来时请直接到官网下载https://github.com/electron/electron/releases 将文件放到 用户目录\AppData\Local\electron\Cache 下 再进行 npm install -g electron
5)	代码中包含native模块，必须进行 rebuild操作
调试渲染进程时增加如下代码增加mainWindow.webContents.openDevTools();

6)	
3.	C++与Python
对于 C++ 和 Python, 遵循 Chromium 的编码风格. 可以使用 clang-format 来自动格式化 C++ 代码. 可以使用 script/cpplint.py 来检验文件是否符合要求。

现在使用的 Python 版本是 Python 2.7。

C++ 代码使用了大量 Chromium 的抽象和类型，因此建议使用者熟悉它们。 一个起步的好地方是 Chromium 的《重要的抽象概念和数据库结构》文档. 该文档提到一些特殊类型，范围类型(超出范围时自动释放其内存), 记录机制等。
4.	命名相关
Electron API 使用与 Node.js 相同的大小写方案：
当模块本身是class时, 比如 BrowserWindow, 使用 大驼峰.
当模块是一组 API 时, 比如 globalShortcut时，使用 小驼峰。
当 API 是对象的属性时, 并且它复杂到足以成为一个单独的块, 比如 win.webContents, 使用 小驼峰.
对于其他非模块API, 使用自然标题, 比如 <webview> Tag 或 Process Object.

当创建新的 API 时， 最好使用 getter 和 setter 而不是 jQuery 的一次性函数。 举个例子, .getText() 和 .setText(text) 优于 .text([text]). 


5.	工程目录结构
src	- main
		// 必须
		- main.js // 入口
		- listen.js // 监听渲染进程通信
		- windows.js // 创建渲染进程
		- log.js // 日志log4js 插件

		// 可选
		- utils.js
		- store.js
- api.js
- render

main 目录下为主进程代码，render 目录下为渲染进程代码
渲染进程目录结构规范与前端项目目录结构规范一致

主进程中必须包含入口文件，监听进程文件和窗口创建文件
其他根据后端实际使用技术可选，nodejs作为后端的话 必须
6.	打包
Electron-packager 绿色可执行包
Electron-builder 压缩安装包

