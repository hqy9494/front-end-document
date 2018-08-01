# 前端文档
博胜前端组项目开发文档规范以及记录问题解决方案

1. 技术栈
2. 前台
3. 后台
4. 提交代码
5. 问题与解决方案

## 一：技术栈
| 技术名称 | 推荐学习链接 |
|:---:|:---:|
| react | [react小书](http://huziketang.mangojuice.top/books/react/) |
| redux | [react小书](http://huziketang.mangojuice.top/books/react/) |
| antd | [antd](https://ant.design/index-cn) |
| antd-mobile | [antd-mobile](https://mobile.ant.design/index-cn) |
| git | [廖雪峰git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000) |
| es6 | [阮一峰](http://es6.ruanyifeng.com/) |
| sass | [官网](https://www.sass.hk/) |

## 二：前台
分为两种项目，假如项目简单不需要太多额外的包或者需要兼容ie8以下（例如落地页），可以使用[web-mobile-cli](https://github.com/sihai00/web-mobile-cli)。
假如项目复杂可以使用[后台框架 + react-keeper](https://git.bosim.cc/luckytea/luckytea-h5)或者dva

### 2.1：简单的项目
| 脚手架 | 教程 |
|:---:|:---:|
| [web-mobile-cli](https://github.com/sihai00/web-mobile-cli) | [使用教程](https://github.com/sihai00/blog/tree/master/2018-04-17/web-mobile-cli%E7%AE%80%E6%98%93%E6%95%99%E7%A8%8B) |

### 2.2：复杂的项目
| 脚手架 | 教程 |
|:---:|:---:|
| [dva](www.baidu.com) | [官方文档](https://github.com/dvajs/dva) |
| [后台框架 + react-keeper](https://git.bosim.cc/luckytea/luckytea-h5) | [react-keeper](https://github.com/vifird/react-keeper) |

## 三：后台
| 脚手架 | 教程 |
|:---:|:---:|
| [项目地址common-web](https://git.yoopin.com.cn/common/common-web.git) | [简易教程](./common-web.md) |

## 四：提交代码
流程：***必须这个流程***
1. 暂存（贮藏）代码
2. 拉取远端代码
3. 释放暂存（贮藏）的代码
4. 解决冲突，保证项目没有问题
5. 提交代码

## 五：问题与解决方案
记录一些平时项目所遇到的问题和解决方案

### 问题1：在手机端调试不方便
解决：[类似浏览器的控制台](https://github.com/liriliri/eruda)

### 问题2：链接转换成二维码
解决：[qrcode](https://github.com/davidshimjs/qrcodejs)
