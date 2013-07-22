---
layout: default_v3
title: qboxrsctl 命令行辅助工具使用文档
version: v3
---


## 简介

qboxrsctl 是根据七牛云存储API实现的一个简易命令行辅助工具。覆盖 [七牛云存储开发者网站](https://dev.qiniutek.com/) 包含的大部分甚至更高级的功能。开发者在对 [七牛云存储 OpenAPI](http://docs.qiniutek.com/v3/api/) 有基本了解的情况下，此工具将会非常适用。

## 下载

qboxrsctl 命令行辅助工具下载地址：

* Mac OS: <http://devtools.qiniudn.com/darwin_amd64/qiniu-devtools.zip>
* Linux 64bits: <http://devtools.qiniudn.com/linux_amd64/qiniu-devtools.zip>
* Linux 32bits: <http://devtools.qiniudn.com/linux_386/qiniu-devtools.zip>
* Windows 32bits: <http://devtools.qiniudn.com/windows_386/qiniu-devtools.zip>
* Windows 64bits: <http://devtools.qiniudn.com/windows_amd64/qiniu-devtools.zip>

## 用法

**授权操作**

- [登录](#login)

**账号管理**

- [查看帐号信息](#info)
- [生成密钥（AccessKey/SecretKey）](#newaccess)
- [查看密钥（AccessKey/SecretKey）](#appinfo)
- [删除密钥（AccessKey/SecretKey）](#delaccess)

**空间管理**

- [创建空间（Bucket）](#mkbucket)
- [将空间设置为公开](#set-bucket-public)
- [将空间设置为私有](#set-bucket-private)
- [列出所有空间（Buckets）](#buckets)
- [查看指定空间（Bucket）信息](#bucketinfo)
- [删除空间（Bucket）](#drop)
- [设置镜像存储（源站加速）](#img)
- [取消镜像存储](#unimg)
- [清除配置缓存](#refresh)
- [设置防盗链](#antiLeechMode)
- [更新黑/白名单记录](#referAntiLeech)

**云处理**

- [添加API规格别名](#style)
- [删除API规格别名](#unstyle)
- [设置友好URL分隔符](#separator)
- [设置源文件/原图保护](#protected)

**文件操作**

- [上传文件](#put)
- [下载文件](#get)
- [查看文件](#cat)
- [复制文件](#cp)
- [移动文件](#mv)
- [删除文件](#del)


qboxrsctl 各个指令的用法可以在命令行直接输入 qboxrsctl 不带参数来获得。

## 1. 授权操作

<a name="login"></a>

### 1.1 登录

    qboxrsctl login <User> <Passwd>

**参数**

`<User>`
: 用户名，一般为注册邮箱

`<Passwd>`
: 登录密码

用您的开发者帐号登录七牛云存储，登录成功后，才能进行接下来所有其他指令操作。

登录成功后，会话的有效期是 3600 秒（一个小时），一个小时后需要重新登录。

## 2. 账号管理

<a name="info"></a>

### 2.1 查看帐号信息

    qboxrsctl info

返回账号信息

<a name="newaccess"></a>

### 2.2 生成密钥（AccessKey/SecretKey）

    qboxrsctl newaccess <AppName>

**参数**

`<AppName>`
: 应用名称，[网站](https://dev.qiniutek.com/account/keys) 上默认创建的应用名称是：`default`

<a name="appinfo"></a>

### 2.3 查看密钥（AccessKey/SecretKey）

    qboxrsctl appinfo <AppName>

**参数**

`<AppName>`
: 应用名称，[网站](https://dev.qiniutek.com/account/keys) 上默认使用的应用名称是：`default`

<a name="delaccess"></a>

### 2.4 删除密钥（AccessKey/SecretKey）

    qboxrsctl delaccess <AppName> <AccessKey>

**参数**

`<AppName>`
: 应用名称，[网站](https://dev.qiniutek.com/account/keys) 上默认使用的应用名称是：`default`

`<AccessKey>`
: 指定要删除掉的 AccessKey

## 3. 空间管理

<a name="mkbucket"></a>

### 3.1 创建空间（Bucket）

    qboxrsctl mkbucket <Bucket>

**参数**

`<Bucket>`
: 空间名称，字母数字下划线组合。

<a name="set-bucket-public"></a>

### 3.2 将空间设置为公开

    qboxrsctl private <Bucket> 0

<a name="set-bucket-private"></a>

### 3.3 将空间设置为私有

    qboxrsctl private <Bucket> 1

<a name="buckets"></a>

### 3.4 列出所有空间（Buckets）

    qboxrsctl buckets

<a name="bucketinfo"></a>

### 3.5 查看指定空间（Bucket）信息

    qboxrsctl bucketinfo <Bucket>

<a name="drop"></a>

### 3.6 删除空间（Bucket）

    qboxrsctl drop -f <Bucket>

<a name="img"></a>

### 3.7 设置镜像存储（源站加速）

    qboxrsctl img <Bucket> <SrcUrl>[,<SrcUrl2>,...] [SrcHost]

**参数**

`<Bucket>`
: 指定用于托管源站资源的存储空间名称，必填。

`<SrcUrl>`
: 源站地址，必填，可设置多个。格式：`http://domain:port/` 或者 `http://ip:port/`，其中 port 可选。

`[SrcHost]`
: 源站域名，可选

<a name="unimg"></a>

### 3.8 取消镜像存储

    qboxrsctl unimg <Bucket>

<a name="refresh"></a>

### 3.9 清除配置缓存

    qboxrsctl refresh <Bucket>

<a name="antiLeechMode"></a>

### 3.10 设置防盗链

    qboxrsctl antiLeechMode <Bucket> <Mode>

**参数**

`<Mode>`
: 可选值为 `0`、`1`、`2` 。 `0`表示不设置防盗链，`1`表示白名单模式，`2`表示黑名单模式。

<a name="referAntiLeech"></a>

### 3.11 更新黑/白名单记录

    qboxrsctl referAntiLeech <Bucket> <Mode> <add|del> <Pattern>

**参数**

`<Mode>`
: 可选值为 `1`、`2` 。`1`表示白名单模式，`2`表示黑名单模式。

`<add|del>`
: `add` 表示添加记录，`del` 表示删除记录

`<Pattern>`
: 标准通配符形式的记录值，比如 `*.example.com`，`12.34.56.*` 等等。


## 4. 云处理

<a name="style"></a>

### 4.1 添加API规格别名

    qboxrsctl style <Bucket> <Name> <Style>

**参数**

`<Name>`
: 别名名称

`<Style>`
: API规格定义，可使用 [图像处理接口](/v3/api/foimg/)、[音频 / 视频处理接口](/v3/api/avfop/)。 

缩略图可以通过如下形式访问：

    http://<Domain>/<Key><Sep><Name>

<a name="unstyle"></a>

### 4.2 删除API规格别名

    qboxrsctl unstyle <Bucket> <Name>

<a name="separator"></a>

### 4.3 设置友好URL分隔符

    qboxrsctl separator <Bucket> <Sep>

<a name="protected"></a>

### 4.4 设置源文件/原图保护

    qboxrsctl protected <Bucket> <Protected>

**参数**

`<Protected>`
: 可选值为 `0` 或者 `1` ，`0`表示不开启保护，`1`表示开启保护。

## 5. 文件操作

<a name="put"></a>

### 5.1 上传文件

    qboxrsctl put <Bucket> <Key> <SrcFile>
    
上传一个大文件（超过 4MB）

    qboxrsctl put -c <Bucket> <Key> <SrcFile>

加上选项 `c`　会启用切片并行上传一个超过大文件。（超过 4MB） 

<a name="get"></a>

### 5.2 下载文件

    qboxrsctl get <Bucket> <Key> <DestFile>

<a name="cat"></a>

### 5.3 查看文件

    qboxrsctl cat <Bucket> <Key>
    
<a name="cp"></a>

### 5.4 复制文件

将 `Bucket1` 中的 `KeySrc` 复制到 `Bucket2` 并命名为 `KeyDest`, `Bucket1` 和 `Bucket2` 可以是同一个。

    qboxrsctl cp <Bucket1:KeySrc> <Bucket2:KeyDest>

<a name="mv"></a>

### 5.5 移动文件

将 `Bucket1` 中的 `KeyOld` 移动到 `Bucket2` 并命名为 `KeyNew`, `Bucket1` 和 `Bucket2` 可以是同一个。

    qboxrsctl mv <Bucket1:KeyOld> <Bucket2:KeyNew>

<a name="del"></a>

### 5.6 删除文件

    qboxrsctl del <Bucket> <Key>
