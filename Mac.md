## Mac 环境变量配置

#### 命令

- `echo $PATH` 输出当前所有的注册的环境变量
- `echo $SHELL` 查看当前使用的`shell`
- `which name` 查看包的安装路径
- `source name` 刷新配置，让配置能够生效
- `npm ls -g` 查看所有全局安装的模块
- `npm config list` 查看`npm config`的配置
- `npm root -g` 查看安装路径是否成功

#### Npm

- `install` 安装失败的解决情况

  - `npm install --registry=https://registry.npm.taobao.org --unsafe-perm`
  - `npm config set unsafe-perm`（针对当前用户的）

  - `npm config -g set unsafe-perm` (全局的）
  - `npm config list -l` 查看当前`npm`的配置

- 改变 Npm 默认的安装路径
  - `mkdir ~/.npm-global` 创建全局安装路径
  - `npm config set prefix '~/.npm-global'` 配置 npm 使用新目录
  - `export PATH=~/.npm-global/bin:$PATH` 在~/.profile 文件增加配置
  - `source ~/.profile`

#### Vim 简单命令

- `:w` 保存但是不退出
- `:wq` 保存并退出
- `:q` 退出
- `:q!` 强制退出，不保存
- `:e!` 放弃修改

#### Nvm

- 为了加速`Node`下载过程,可以在`.bashrc`增加如下配置
  - `export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node`
  - **不要忘记 `source .bashrc`**
- 说明
  - default nvm 默认使用的版本
  - node 和 stable 当前安装的 node 的最新的稳定版本
  - iojs iojs 的最新稳定版本
  - lts/\* node lts 系列最新的稳定版本
  - lts/argon,lts/boron,lts/carbon 分别指 lts 的三个大的版本的最新版本
- 切换临时版本
  - `nvm use xxx 或 nvm use lts/dubnium`
  - 长期切换版本（关掉当前控制台 tab，下次依旧生效）：
    - `nvm alias default xxx

* 遇见的问题
  - nvm 和 npm prefix 冲突 https://my.oschina.net/yangq20/blog/768281

#### [nrm](https://github.com/Pana/nrm)

- 全局安装
  - `npm install -g nrm`
- 查看所有可用的源
  - `nrm ls`

* 添加源
  - `nrm add 名称`
* 删除原
  - `nrm del 名称`
* 切换源
  - `nrm use 名称`
* 测试速度
  - `nrm test`
