title: package.json字段
tags: 'webpack'
categories: 'node'
---
### package.json里的各个字段

#### 概述
项目的根目录中一般有一个package.json文件，定义了这个项目所需要的各种模块，以及项目的配置信息。npm install命令根据这个配置文件，自动下载所需的模块。
<!-- more -->

#### scripts字段
scripts指定了运行脚本命令的npm命令行缩写。例如，start制定了运行npm run start时，所要执行的命令。

#### dependencies字段，devDependencies字段
dependencies字段指定了项目运行所依赖的模块，devDependencies字段指定项目开发所需要的模块。

#### peerDependencies
peerDependencies字段用来供插件指定其所需要的主工具的版本。
```
{
    "name": "chai-as-promised",
    "peerDependencies": {
        "chai": "1.x"
    }
}
```

#### bin字段 【非必须】
bin项用来指定各个内部命令对应的可执行文件的位置

#### main字段
main字段指定了加载的入口文件，require('moduleName')就会加载这个文件，这个字段的默认值是模块根目录下面的index.js。

#### config字段
config字段用于添加命令行的环境变量。
```
{
    "name": "foo",
    "config": {"port" : "8080"}，
    "scripts" : {
        "start" : "node server.js"
    }
}
```
然后，在server.js脚本就可以引用config字段的值。