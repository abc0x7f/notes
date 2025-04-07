# 环境配置 <!-- omit from toc -->

- [命令行](#命令行)
  - [cmd(windows)](#cmdwindows)
- [标记语言](#标记语言)
  - [markdown](#markdown)
  - [LaTex(待完成)](#latex待完成)
- [g++](#g)
  - [下载安装](#下载安装)
  - [配置环境变量](#配置环境变量)
  - [使用](#使用)
- [代码编辑器](#代码编辑器)
  - [vscode](#vscode)
    - [安装**vscode**(微软商店) - 不能有中文路径](#安装vscode微软商店---不能有中文路径)
    - [创建工作区并信任 - 不能有中文路径](#创建工作区并信任---不能有中文路径)
    - [下载插件](#下载插件)
    - [json配置](#json配置)
    - [使用](#使用-1)
  - [Vim](#vim)
    - [安装 vim.org, 配置环境变量](#安装-vimorg-配置环境变量)
    - [vim主题 wwdc16 置于 *C:\\Program Files\\Vim\\vim82\\colors*](#vim主题-wwdc16-置于-cprogram-filesvimvim82colors)
    - [.vimrc](#vimrc)
    - [基本操作](#基本操作)
    - [语法](#语法)
  - [Sublime(待完成)](#sublime待完成)


# 命令行

## cmd(windows)
```sh
:: 注释内容
. 表示当前目录, .. 表示父目录
当前目录下的fo文件夹为 .\fo\, 父目录下的a文件为 ..\a
cd {dirpath}\{dirname} 进入该目录的 {dirname} 文件夹
md folder / mkdir folder 创建名为folder的文件夹
dir 显示当前目录的文件列表
(powershell only) ls 显示当前目录的文件列表

rd folder 删除当前目录名为folder的空文件夹
rd /s folder 删除folder和该目录下的所有文件
del file 删除名为file的文件
ren A B 将文件A重命名为B
fc {fileA} {fileB} 比较文件A与文件B内容

(cmd only) {comandA} && {comandB} 执行命令A后执行命令B
(powershell only) {comandA} ; {comandB} 执行命令A后执行命令B
(except cmd) .\a.exe 执行a.exe(非cmd中当前目录默认不在搜索环境中所以要注明)
```

# 标记语言

## markdown
```markdown
# 一级标题
## 二级标题
### 三级标题
**粗体**
*斜体*
~~删除线~~
![desciption](url) 插入图片
[description](url) 插入链接
<url> 插入网址
<p> </p> 插入段落
<br /> 换行

- 无序列表
- 无序列表
- 无序列表

[链接文本][链接标识] 引用式超链接
[链接标识]: https://example.com
```
```md
` 行内代码 `
```{codetype}
代码块
​```

块引用
> line1
> line2
> line3

$ 行内公式 $
$$
公式块
$$

表格
|      |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |
```
```markdown
- [x] 任务状态已完成
- [ ] 任务状态未完成

{正文}[^footnote] 脚注
[^footnote]: 脚注内容

<!-- 注释 -->
<!-- omit from toc --> 生成目录时忽略
```

## LaTex(待完成)

# g++
## 下载安装 
[Donwload from Winlib](https://winlibs.com/) 选择**ucrt,** **posix** (通用运行库,通用线程)
## 配置环境变量
## 使用
```shell
g++/clang++ -g {filename}.cpp -o {filename}.exe
g++ -g {filename}.cpp -o {filename}.exe -O2 -Wall -fdiagnostics-color=always
```
```shell
参数
-g  启用gdb调试
-o  输出为
-O2 启用O2优化
-Wall 打开警告文件
-lm 引用数学库
-DONLINE_JUDGE 申明为在线评测

(g++ only) -fdiagnostics-color=always 报错信息上色
(clang++ only) -fcolor-diagnostics    报错信息上色
```

# 代码编辑器

## vscode
### 安装**vscode**(微软商店) - 不能有中文路径
### 创建工作区并信任 - 不能有中文路径
```
(vscode) > Workspace: Manage Workspace trust
```
### 下载插件
```
Chinese (Simplified) by Microsoft
C/C++ _by Microsoft
C/C++ Extension Pack _by Microsoft
C/C++ Compile Run _by danielpinto8zz6 (F6一键编译并运行,独立控制台)
Markdown All in One _by Yu Zhang
```
### json配置
```json
//task.json - 任务
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C++_runinter", // 任务(标签)名
            "command": "",
            "args": ["${fileDirname}\\${fileBasenameNoExtension}.exe"],
            "options": {
                "cwd": "${fileDirname}" // 执行目录(当前文件夹)
            },
            "dependsOn": [ // 依赖的任务
                "C++_compile",
            ],
            "problemMatcher": [],
            "group": {
                "kind" : "build", // 组名
                "isDefault": true // 组中默认(按Ctrl + shift + b默认执行)
            },
            "detail": "运行文件",
            "presentation": {
                "echo": true, //终端消息
                "reveal": "always", // 显示终端
                "focus": true, // 焦点终端
                "panel": "new" // 终端模式(新开 / 共用 / 沉默)
            }
        },
        {
            "type": "cppbuild",
            "label": "C++_compile", // 任务(标签)名
            "command": "D:\\mingw64\\bin\\g++.exe",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe",
                "-O2",
                "-Wall"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [ //错误信息显示类型
                "$gcc"
            ],
            "group": {
                "kind": "build",
                //"isDefault": true
            },
            "detail": "调试器生成的任务。",
            "presentation": {
                "echo": true,
                "reveal": "always",
                "focus": true,
                "panel": "new"
            }
        }
    ],
    "version": "2.0.0"
}
```
```json
//launch.json - 调试
{
    "configurations": [
        {
            "name": "C++_run",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [";pause"], // 暂停终端(目前无用)
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": true, // 启用独立终端
            "MIMode": "gdb",
            "miDebuggerPath": "D:\\mingw64\\bin\\gdb.exe", // 调试程序目录
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],
            
            "presentation": {
                "echo": true,
                "reveal": "always",
                "focus": true,
                "panel": "new"
            },
            "preLaunchTask": "C++_compile" // 前置任务
        },
    ],
    "version": "2.0.0"
}
```
### 使用
1. 快捷键 <br />
**Ctrl + p**, 直接输入以搜索文件, 输入 **>** 以执行命令, 输入 **%** 以搜索文本 <br />
**Ctrl + shift + p**, 执行命令 <br />

## Vim
### 安装 [vim.org](https://vim.org), 配置环境变量
### vim主题 [wwdc16](notes/quote/wwdc16.vim) 置于 *C:\Program Files\Vim\vim82\colors*
### .vimrc
[Windows](./quote/_vimrc)
[Linux](./quote/__vimrc[linux])
```vim
(Windows) 放置于 X:\Program Files\Vim (Vim安装路径, X为盘符)

set nobackup " 无备份文件
set noundofile " 无永久性可撤回文件
" set noswapfile " 无交换文件(断电保护)
需注释掉source $VIMRUNTIME/vimrc_example.vim
```
### 基本操作
```vim
按 i 进入插入(编辑)模式
按 <Esc> 进入命令模式
命令模式下,
按 : 以键入命令
按 / 以匹配文本
```
```vim
:w 保存 :w! 强制保存
:q 退出 :q! 强制退出
:sp 水平分屏 :vsp 垂直分屏
:o {filename} 打开文件
:!{command} 在终端执行命令
:!g++ -g % -o %< -Wall -O2 编译cpp文件
:!%< 执行文件
```
### 语法
```vim
命令语法
{vimcomand1} | {vimcomand2} 先1再2
{vimcomand1} | !{terminalcomand2} && {terminalcomand3} 先1再2再3
% or .\% 当前文件名
%< or .\%< 当前文件名(无扩展)
```
```vim
.vimrc语法
" {description} 注释
" 函数写法
func! {funcname}()
    exec "{vimcomand1} | {vimcomand2} | !{terminalcomand3}" 先1再2再3, exec为命令模式中执行
endfuc

imap<KEY1> <KEY2> :!{terminalcomand} <CR>
" 插入模式中,按下KEY1产生按KEY2与终端中执行命令1的效果
map<KEY1> <KEY2> :call {funcname}() <CR>
" 命令模式中,按下KEY1产生按KEY2与执行函数的效果

 call setline(1, "...") 将文件第1行变为...的内容
 call append(line("."), "....") 将下一行变为....的内容, 可重复
```

## Sublime(待完成)