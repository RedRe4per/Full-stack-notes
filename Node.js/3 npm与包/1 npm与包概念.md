### Node.js 3.1 npm与包概念

1. **包**

   Node.js 中的第三方模块又叫做包（只是叫法不同）。包是基于内置模块封装出来的，提供了更高级，更方便的API，极大的提高了开发效率。

   包的来源：包是由第三方个人或团队开发出来的，免费供所有人使用。Node.js 中的包都是免费和开源的。包的下载网站是 [npm](https://www.npmjs.com/)，它是全球最大的包共享平台。npm 的服务器地址是 http://registry.npmjs.org/ ，不能直接打开但是可以使用工具下载包。

   这个包管理工具的名字叫做 Node Package Manager，简称 npm 包管理工具，这个包管理工具随着 Node.js 的安装包一起被安装到了用户电脑上。可以在终端中执行 `npm -v` 命令来查看版本号。

   

2. **在项目中安装包**

   `npm install 包的完整名称` ：项目中安装包（最新版本）。执行时会把包名和版本号记录至 package.json。

   `npm i 包的完整名称` ：安装包，简写。

   包的用法可以去 npmjs 上搜索包名，找到 Documentation，就是说明文档。

   

   `@` 符号：安装指定版本的包。 例如 `npm i moment@2.22.2` 。如果是已安装过其他版本的包，想重新安装，也不需要卸载原版本包，而是直接执行新指令即可。

   包的语义化版本规范：第一位数字是大版本，第二位数字是功能版本，第三位数字是 bug 修复版本。版本号提升的规则是，只要前面的版本号增长了，则后面的版本号归零。

   

3. **初次装包后：node_modules 和 package-lock.json**

   初次装包后，在项目文件夹下多一个叫做 node_modules 的文件夹和 package-lock.json 的配置文件。

   **<font color='green'>node_modules 文件夹 </font>**用来<font color='red'>存放</font>所有已经安装到项目中的包。`require()` 导入第三方包时，就是从这个目录中查找并加载包。

   **<font color='green'>package-lock.json 配置文件</font>** 用来<font color='red'>记录</font> node_modules 目录下每一个包的下载信息，如包名，版本号，下载地址。

   <font color='red'>注意：不要手动修改 node_modules 和 package-lock.json 的任何代码，npm 包管理工具会自动维护。</font>

   

4. **包管理配置文件：package.json**

   npm 规定，在项目根目录中，必须提供一个叫做 **<font color='green'>package.json</font>**  的包管理配置文件，用来记录与项目有关的配置信息：

   + 项目的名称、版本号、描述等

   + 项目中都用到了哪些包
   + 哪些包只在开发期间会用到
   + 哪些包在开发和部署时都需要用到

   

   多人协作的问题

   第三方包体积过大。比如整个项目体积 30.4M，第三方包 28.8M，项目源代码体积 1.6M。这样不便于团队成员之间共享项目源代码。

   解决方案：我们共享时只上传源代码（1.6M），剔除 node-modules，其他人从网上下载第三方包即可。但是怎么让其他人知道我们用了哪些第三方包呢？

   记录项目中的包：package.json 配置文件，用来记录项目安装了哪些包。这样剔除 node-modules 后，团队成员之间可以共享项目源代码。

   注意：项目开发中，一定要把 node_modules 文件夹添加到 .gitignore 忽略文件中。

   

   快速创建 package.json

   `npm init -y` 在执行命令所处的目录中，会所新建 package.json 文件。<font color='red'>在新建项目文件夹后，第一件事就是先执行这个命令，并且在项目开发期间只需要执行唯一一次。</font>

   注意上述命令只能在英文目录下成功运行，因此项目文件夹不要出现中文和空格。`npm install 包的完整名称` 安装命令执行时会把包名和版本号记录至 package.json。

   

5. **dependencies 节点**

   当运行 `npm install 包的完整名称` 命令后，package.json 文件中就会创建 dependencies 节点了。它用来记录使用 `npm install 包的完整名称` 命令安装了哪些包。

   

6. **一次性安装所有包**

   当我们拿到一个剔除了 node_modules 的项目之后，需要先把所有的包下载到项目中，才能将项目运行，否则会报以下错误：

   ```powershell
   Error: Cannot find module 'moment'
   ```

   可以运行 `npm install` （简写 `npm i`）一次性安装所有的依赖包。

   

7. **卸载包**

   `npm uninstall 包的完整名称` 这个命令可以卸载指定的包，此命令无简写。用这个命令卸载成功后，会把卸载的包从 package.json 的 dependencies 中移除掉。

   

8. **devDependencies 节点**

   如果某些包只在项目开发阶段会用到，在项目上线之后不会用到，则建议把这些包记录到 devDependencies 节点中。与之对应，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。

   `npm install 包名 --save-dev` 命令可以将包记录到 devDependencies 节点中。简写为 `npm i 包名 -D `。

   