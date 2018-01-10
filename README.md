# pfgit
随着公司的发展，项目的功能越来越多，代码也越来越乱，为了解决这个问题公司一般会选择模块化开发，
模块化开发势必会增加大量的仓库，开发面对大量的仓库，任意一个git操作可能都会花费比以前指数倍的时间，
针对这个问题pfgit应运而生。pfgit可以允许开发批量操作git仓库。
#### 用法：
只需要在命令行敲下 python pfgit.md -h即可获取所有功能

#### 注意点
1. pfgit需要一个配置文件，配置文件的内容包含仓库名称、远程地址、分支名称，示例：config.cfg
```
[ManagerApp]
ManagerApp = git@git.2dfire-inc.com:background_manage_new/background-rest_phone.git
ManagerAppName = ManagerApp
ManagerAppBranch = develop

# 登录模块
[LoginModule]
LoginModule = git@git.2dfire-inc.com:tdf_module_android/TDFLoginModule.git
LoginModuleName = LoginModule
LoginModuleBranch = develop

# 掌柜基础模块
[ManagerBase]
ManagerBase = git@git.2dfire-inc.com:background_manage_android/ManagerBase.git
ManagerBaseName = ManagerBase
ManagerBaseBranch = develop
.
.
.
```
2. 项目主工程和依赖的library必须在同一级文件夹，pfgit和配置文件必须放在项目的根目录
3. 目前支持的功能有批量拉取、批量提交、批量切换等有限的功能，还在继续开发中。。。

#### 示例：
1. 切分支：python pfgit.md -c 或者 python pfgit.md --checkout=develop
2. 拉分支：python pfgit.md -p 或者 python pfgit.md --pull
.
.
.
#### 命令行修改（unix）
先执行 chmod +x pfgit.md
以后可通过 ./pfgit.md 使用pfgit的功能