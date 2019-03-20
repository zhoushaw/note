## 依赖环境配置


> yarn 


```
vim .zshrc
export PATH="$PATH:`yarn global bin`"
```

## 配置

运行 npm config set loglevel http，让你知道 npm 发的每一个请求
运行 npm config set progress false，关闭那个进度条
为了让你的安装速度变快，运行 npm config set registry https://registry.npm.taobao.org/
想要恢复成原样，只需要 npm config delete registry 即可

## --save-dev --save 的区别

npm install 在安装 npm 包时，有两种命令参数可以把它们的信息写入 package.json 文件，一个是npm install--save另一个是 npm install –save-dev，他们表面上的区别是--save 会把依赖包名称添加到 package.json 文件 dependencies 键下，--save-dev 则添加到 package.json 文件 devDependencies 键
不过这只是它们的表面区别。它们真正的区别是，npm自己的文档说dependencies是运行时依赖，devDependencies是开发时的依赖。即devDependencies 下列出的模块，是我们开发时用的，比如 我们安装 js的压缩包gulp-uglify 时，我们采用的是 “npm install –save-dev gulp-uglify ”命令安装，因为我们在发布后用不到它，而只是在我们开发才用到它。dependencies 下的模块，则是我们发布后还需要依赖的模块，譬如像jQuery库或者Angular框架类似的，我们在开发完后后肯定还要依赖它们，否则就运行不了。


## npm代理设置

> 起步

`vim ~/.npmrc`

> 切换代理

```
registry=https://registry.npm.taobao.org
//registry=http://npm.f2e.mogujie.org/
//registry=https://registry.npmjs.org/
```

## 端口占用查询

> 查询端口占用

`lsof -i:3000`


> 解除端口占用(PID在查询端口出现)

`sudo kill -9 PID`





## 本地调试npm包


<p class="tip">在开发npm包的过程中，难免会发生问题，每次更改测试都需要重新publish十分麻烦，可以通过将npm包直接link到项目中，解决完bug后，再publish无疑是十分高效的处理方法</p>


使用：

```
npm link (in package dir)
npm link [<@scope>/]<pkg>[@<version>]
```

当完成npm包调试后，


```
npm unlink
```

