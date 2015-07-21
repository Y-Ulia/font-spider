#	字蛛

中文 WebFont 自动化压缩工具，它能自动分析页面使用的 WebFont 并进行按需压缩。

官方网站：<http://font-spider.org>

## 特性

相对于图片，WebFont 拥有更好的体验。它支持选中、搜索、翻译、朗读、缩放等，而字蛛作为一个 WebFont 压缩转码工具，拥有如下特性：

1. 按需压缩：数 MB 的中文字体可被压成几十 KB
2. 简单可靠：完全基于 CSS 规则，无需 js 与服务端辅助
3. 自动转码：支持 IE 与标准化的浏览器

##	安装

安装好 [nodejs](http://nodejs.org)，然后执行：

```
npm install font-spider -g
```

##	使用范例

### 一、书写 CSS

```
/*声明 WebFont*/
@font-face {
  font-family: 'pinghei';
  src: url('../font/pinghei.eot');
  src:
    url('../font/pinghei.eot?#font-spider') format('embedded-opentype'),
    url('../font/pinghei.woff') format('woff'),
    url('../font/pinghei.ttf') format('truetype'),
    url('../font/pinghei.svg') format('svg');
  font-weight: normal;
  font-style: normal;
}

/*使用选择器指定字体*/
.home h1, .demo > .test {
    font-family: 'pinghei';
}
```

> 特别说明： `@font-face` 中的 `src` 定义的 .ttf 文件必须存在，其余的格式将由工具自动生成

###	二、压缩 WebFont

```
font-spider [options] <htmlFile ...>
```

> 支持通配符，例如：`font-spider dest/*.html`

#### options

```
-h, --help                    输出帮助信息
-V, --version                 输出当前版本号
--info                        仅提取 WebFont 信息显示，不压缩与转码
--ignore <pattern>            忽略的文件配置（可以是字体、CSS、HTML）
--map <remotePath,localPath>  映射 CSS 内部 HTTP 路径到本地
--no-backup                   关闭字体备份功能
```

## 前端构建工具集成

* [grunt-font-spider](https://github.com/aui/grunt-font-spider)
* [gulp-font-spider](https://github.com/aui/gulp-font-spider)

## 字蛛限制

* 不支持元素行内样式（只支持 `<link>` 与 `<style>` 标签声明的样式）
* CSS `content` 属性插入的字符需要定义 `font-family`，不支持继承
* 不支持 javascript 动态插入的样式与元素节点
* 不支持 .otf 格式的字体

## 字体兼容性参考

格式 | IE | Firefox | Chrome | Safari | Opera | iOS Safari | Android Browser | Chrome for Android 
----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | -----
`.eot` | 6  | -- | -- | -- | -- | -- | -- | --
`.woff` | 9 | 3.6 | 5 | 5.1 | 11.1 | 5.1 | 4.4 | 36 
`.ttf` | --  | 3.5 | 4 | 3.1 | 10.1 | 4.3 | 2.2 | 36
`.svg` | -- | -- | 4 | 3.2 | 9.6 | 3.2 | 3 | 36

来源：<http://caniuse.com/#feat=fontface>

## 更新日志

### 0.3.0

* 重构爬虫模块，解决压缩后的 CSS 解析失败的问题
* 同名字体支持 [#32](https://github.com/aui/font-spider/issues/32)
* 改进错误流程处理：HTML、CSS 加载与解析错误都会进入错误流程

### 0.2.1

* 避免部分字体转码失败导致程序崩溃的问题 [#28](https://github.com/aui/font-spider/issues/28)
* 使用隐藏目录`.font-spider`备份字体

### 0.2.0

* 使用 fontmin 取代字蛛内置的压缩与转码模块，让压缩后的字体更小，并且无需 Perl 环境 [#18](https://github.com/aui/font-spider/issues/18)
* 优化爬虫模块，使用更高效的 cheerio 代替 jsdom 解析 HTML
* 支持解析远程动态页面，可结合`map`参数映射线上 CSS 与 WebFont 资源到本地
* 实现对 CSS `:before`与`:after`定义`content`的支持（不支持继承的字体）

### 0.1.1

* 修复和最新版 NodeJS 兼容问题

### 0.1.0

* 优化错误信息显示
* 支持`map`配置映射 CSS 文件中的 http 路径到本地目录
* 支持`ignore`配置忽略字体、CSS、HTML 文件
  
### 0.0.1

* 基于 CSS 规则压缩与转码 WebFont

## 贡献者 

字蛛诞生离不开这三位小伙伴，他们是：

* [@糖饼](https://github.com/aui) [微博](http://www.weibo.com/planeart)
* @fufu [微博](http://www.weibo.com/u/1715968673)
* @kdd [微博](http://www.weibo.com/kddie)

### 特别鸣谢

字蛛自 v0.2 版本开始，使用了百度前端团队开源作品 —— [fontmin](https://github.com/ecomfe/fontmin) 取代了字蛛内置的字体压缩库。字蛛希望与更多的人或团队一起合作，为中文 WebFont 的发展出一份力！

=============

*字体受版权保护，若在网页中使用商业字体，请联系相关字体厂商购买授权*

[![NPM](https://nodei.co/npm/font-spider.png?downloads=true&stars=true)](https://nodei.co/npm/font-spider/)