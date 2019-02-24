# miniprogram-build [![npm version](https://badge.fury.io/js/miniprogram-build.svg)](https://www.npmjs.com/package/miniprogram-build) [![Greenkeeper badge](https://badges.greenkeeper.io/NewFuture/miniprogram-build.svg)](https://greenkeeper.io/)

A command line tool to build & watch MiniProgram.

![task flow](https://user-images.githubusercontent.com/6290356/53295020-e13b7f00-382c-11e9-8662-5a5f5dcaeab9.png)

## Usage

### quick start

show all commands

```
npx miniprogram-build -h
```

### install as devDependence

```
npm i miniprogram-build -D
```

### CLI

> `miniprogram-build [command...] [--option]`

Commands:

```
dev      build and watch <构建和检测文件修改>
watch    watch file changes <监测文件变化>
build    clean and compile <清理和编译所有文件>
clean    remove all files in dist <清理dist>
compile  compile all source files to dist <编译所有源文件>
js       compile ts/js files to `.js` <编译生成js>
wxs      compile wxts/wxs files to `.wxs` <编译生成wxs>
wxss     compile scss/sass/css/wxss to `.wxss` <编译生成wxss>
wxml     compile html/wxml files to `.wxml` <编译生成wxml>
json     compile all json/jsonc files to `.json` <编译生成json>
image    compresse all images in source to dist <压缩所有图片>
copy     copy all files match `copy` to dist <复制需要复制的文件>
npm      build npm dependencies to dist <编译npm依赖>
```

Options:

```
  --version     show version number <查看本版号>                       [boolean]
  --release     production mode <发布模式会优化压缩>  [boolean] [default: false]
  --src         source folder <源文件目录>           [string] [default: "src"]
  --dist        output folder <编译输出目录>        [string] [default: "dist"]
  --exclude     ignored files <编译忽略文件(夹)>                         [array]
  --tsconfig    typescript config file <TS配置,未设置会自动查找tsconfig.json>
  --copy        files to copy <复制的文件>
  --assets      assets folder under src/ for compling style, wont put to dist
                <样式所需资源文件;会监测文件修改,但不会编译或复制到输出目录>
                                                    [string] [default: "assets"]
  --var         KEY value pair to replace in js/json <替换JS和JSON中的变量>
  -c, --config  JSON config file <配置置文件,命令参数优先级高于配置>
  -h, --help    show help <显示帮助信息>                               [boolean]
```

examples

-   dev in int env

```
mp-build dev --config=./config.int.json
```

-   build for prod release

```
mp-build build --config=./config.prod.json --release
```

### default config

```json
{
    "release": false,
    "src": "src",
    "dist": "dist",
    "assets": "assets",
    "copy": "",
    "exclude": [],
    "tsconfig": "tsconfig.json",
    "var": {
        "APP_ID": "all {{APP_ID}} in json/ts files will replaced by this value"
    }
}
```

### commands & options

![commands & options](https://user-images.githubusercontent.com/6290356/53218418-07c7b180-3697-11e9-986b-acac08871bdc.png)

### tips

* npm dependences need build npm via devtools (安装外部npm依赖需要开发工具并点击构建npm)
* CSS npm packags install as devDependences with `npm i -D` (CSS的 npm 依赖使用`npm i -D`方式安装)


## Features

* `js`
    * [x] compile `TS`
    * [x] sourcemaps
    * [x] replace `{{var}}`
    * [x] build break
    * [x] JS support
    * [x] error report
    * [ ] tree shaking
    * [ ] one tslib
* `wxss`
    * [x] compile
        * `scss`/`sass`
        * `css`
    * [x] import `node_modules`
    * [x] sourcemaps
    * [x] minify (release) / expanded (debug)
    * [x] inline image
    * [x] inline svg
    * [x] PostCSS 
        * autoprefixeer
        * cssnano & inline svg compress
    * [x] keep import wxss (MUST start with `/` and end with `.wxss`)
    * [x] build break when Invalid
    * [ ] ~~skip local scss `_`~~
    * [x] assest folder
    * [x] error report
* `wxml`
    * [x] `wxml`
    * [x] `html`
    * [x] copy rename
    * [x] compress
    * [x] error report
* `JSON`
    * [x] comments (添加注释)
    * [x] trailing comma
    * [x] minify
    * [x] replace `{{var}}`
    * [x] error report
* resource
    * [x] copy/src
    * [x] image compress
    * [x] error report
* console verbose
    * [x] all files
    * [x] file size


## Todo
* [x] exclude path
* [x] multi watcher
* [ ] ~~init~~
* [x] config
* [x] 显示报错位置
* [x] break errors
* [ ] ~~pages config~~
* [x] [template project](https://github.com/NewFuture/miniprogram-template)
* [ ] cache
* `svg` ==> `iconfonts`
    * [ ] svg ==> iconfont 
    * [ ] build wxss
* miniprogram native npm
    * [x] link node_modules
    * [ ] rollup js lib
    * [ ] components
