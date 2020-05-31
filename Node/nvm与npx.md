## Nvm 是什么？

- `Nvm`可以作为`Node`的版本管理工具，可以兼容任意平台，例如`macOs`,`unix`,`Windows`

### 使用方式

- 下载最新版本的`node`可以使用

```
nvm install node
```

- 下载指定版本的 Node`node`

```
nvm install x.x.x
```

- 查看可用的`node`版本信息

```
nvm ls-remote
```

- 使用指定版本的`node`

```
nvm use x.x.x
```

- 获取指定版本的安装路径

```
nvm x.x.x
```

## Npx

- `Node`自带的`npx`模块，可以直接使用`npx`的命令
- 如果`npx`命令不存在，则手动安装

```
npm install -g npx
```

- 主要解决的问题，就是调用项目内部安装的模块

* 如果我们想调用项目内部安装的`webpack`，可能会使用 `./node_modules/.bin/webpack`，而 npx 解决的问题，就是让调用更加方便，可以直接使用`npx webpack`调用即可

* `npx`会直接到项目的`./node_modules/.bin`路径和`$PATH`环境变量检查命令是否存在
* `npx`也会检查系统变量是否存在，例如 `npx ls`
