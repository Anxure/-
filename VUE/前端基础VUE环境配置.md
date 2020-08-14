### 一、Node.js开发环境搭建
1. nvm的安装与使用
    - nvm简介
        
        <p>nvm全称Node Version Manager是 Nodejs 版本管理器，能方便对Nodejs的版本进行切换。 nvm的官方版本只支持Linux和 Mac。 Windows用户，可以用nvm-windows。详情请查看官方说明。</p>
    - 参考链接：
        - [http://blog.csdn.net/tyro_java/article/details/51232458](http://blog.csdn.net/tyro_java/article/details/51232458) 
        - [https://wordpresshi.com/nvm-and-nrm/](https://wordpresshi.com/nvm-and-nrm/) 
        - [http://www.cnblogs.com/zuojiayi/p/6898259.html](http://www.cnblogs.com/zuojiayi/p/6898259.html)
        - [http://blog.csdn.net/qq_27626333/article/details/77857223](http://blog.csdn.net/qq_27626333/article/details/77857223)
    - nvm安装
        - 下载nvm包。下载地址：[nvm-windows下载](https://github.com/coreybutler/nvm-windows/releases)，选择nvm-noinstall.zip下载完成后解压安装目录，比如: D:\development\nvm， 里面的文件有：elevate.cmd、elevate.vbs、install.cmd、LICENSE、nvm.exe
    
        - 双击install.cmd，然后提示输入“压缩文件解压或拷贝到的一个绝对路径” 先不用设置，直接回车，成功后，会在C盘的根目录生成一个settings.txt文件，把这个文件剪切到D:\development\nvm目录中，然后按照如下内容修改：
        ```
          root: D:\development\nvm 
          path: D:\development\nodejs 
          arch: 64
          proxy: none
          node_mirror: http://npm.taobao.org/mirrors/node/ 
          npm_mirror: https://npm.taobao.org/mirrors/npm/
        ```
        
        - 设置环境变量，因为点击了install.cmd的文件，会在环境变量的系统变量中，生成两个环境变量：NVM_HOME 和 NVM_SYMLINK 修改这两个变量名的变量值：NVM_HOME的变量值为：D:\development\nvm ； NVM_SYMLINK的变量值为：D:\development\nodejs
    
        - 默认在Path中也会自动添加上D:\development\nvm;或者是D:\development\nodejs，如果有的话，先删掉，然后在Path的最前面输入： ;%NVM_HOME%;%NVM_SYMLINK%;
        
        - 打开cmd窗口输入命令：nvm version ，查看当前nvm的版本信息。如果正常显示版本号，就可以安装nodejs了，否则需要检查以上安装配置是否正确。
    
        - 继续输入命令：nvm install latest 如果网络畅通，会看到正在下载的提示，下载完成后便能够use那个最新的node版本。
    
        - 如果是第一次下载，在use之前，D:\development目录下是没有nodejs这个文件夹的，在输入比如： nvm use 6.10.0 之后，在D:\development目录下便会创建一个nodejs文件夹，这个文件夹是一个快捷方式，指向了D:\development\nvm 里的v6.10.0文件夹。
        
        - 同样可以下载其他版本的nodejs，通过命令：nvm use 版本号 比如：nvm use 6.10.0就能切换不同版本
        
        - 备注： 如果电脑系统是32 位的，那么在下载nodejs版本的时候，一定要指明 32 如： nvm install 6.10.0 32 这样在32位的电脑系统中，才可以使用，默认是64位的。
    - nvm常用命令
    ```
    nvm install # 安装指定版本，可模糊安装，如：安装v6.2.0，既可nvm install v6.2.0，又可nvm install 6.2
    nvm uninstall # 删除已安装的指定版本，语法与install类似
    nvm use # 切换使用指定的版本node
    nvm ls # 列出本地所有安装的版本
```
    
2. npm的安装与使用

    - 配置npm的全局安装路径，进入cmd，输入 npm config set prefix “D:\development\npm” 回车，然后在用户文件夹下会生成一个.npmrc的文件，用记事本打开后可以看到如下内容：
    ```
    prefix=D:\development\npm
    ```
    
    - 然后安装一个全局nodejs模块，在cmd中输入：npm install grunt -g 回车后会发现正在下载grunt包，在D:\development\npm目录中可以看到下载中的文件，以后只要用npm安装包的时候加上 -g 就可以把包安装在刚刚配置的全局路径下。
    
    - 为npm配置环境变量，在系统变量中新建环境变量：变量名为：NPM_HOME，变量值为 ：D:\development\npm
    
    - 在Path的最前面添加;%NPM_HOME%，注意：一定要添加在%NVM_SYMLINK%之前
    
    - 配置完成后，新打开一个cmd窗口，输入npm -v便能够使用npm安装包了。

3. nrm的安装与使用
    <p>nrm(npm registry manager )是npm的镜像源管理工具，有时候国外资源太慢，可以用这个工具来切换镜像源。</p>
    
    - 全局安装nrm：npm install -g nrm
    - 安装后就可以使用nrm的相关功能，列出可使用的资源：nrm ls，会显示如下内容：
    ```
      npm ---- https://registry.npmjs.org/
      cnpm --- http://r.cnpmjs.org/
    * taobao - https://registry.npm.taobao.org/
      nj ----- https://registry.nodejitsu.com/
      rednpm - http://registry.mirror.cqupt.edu.cn/
      npmMirror  https://skimdb.npmjs.com/registry/
      edunpm - http://registry.enpmjs.org/
    ```
    - 选择淘宝的源：nrm use taobao