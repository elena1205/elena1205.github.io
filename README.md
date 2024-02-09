# 搭建单机魔兽

参考：
1、https://trinitycore.info/ 服务端搭建，英文版，详细
2、https://zhuanlan.zhihu.com/p/671410997 知乎网友翻译，做了一定的精简
3、https://www.dkpminus.com/blog/wow-3-3-5a-download-wrath-of-the-lich-king-client/ 客户端下载与配制，英文版

我是按照参考1中服务端搭建方法一步步执行的，对于其中英文理解有些不确定的参考一下知乎文章，按照步骤执行应该没有什么大问题，可以正确配置，
但是有的时候会遇到明明我就是按照步骤说明执行却怎么不成功的疑惑，以下就是我安装过程中遇到的疑惑，或者说记录下我踩过的一些坑。

1、cmake 配置时候出错
cmake如果GUI需要点击config，命令行就是 cmake <CMakeLists.txt路径>，我遇到的问题是找不到OPEN_SSL_ROOT类似错误，
这个其实纯属个人问题，原文中明确说明 “找到非 "light" 版本”，我在下载的时候看到有light和非light，因为提供了exe版本和msi版本，我先去查了一下exe和msi的区别，回头再下载的时候一不留神下载了light版本，弄了好久终于发现是light版本，重新换了非light版本就成功了。

2、使用visual studio编译报错
cmake配置成功后生成vsstudio工程，编译的时候报错，和boost相关，原因是比如下载的boost版本为 boost_1_80_0-msvc-14.3-64.exe，1_80是boost版本，msvc-14.3是对应的visual studio版本，这个在英文版中有说明，知乎的翻译文档中没有。
If you prefer a higher Boost version check here: https://sourceforge.net/projects/boost/files/boost-binaries/
Not all version are currently supported by TrinityCore (minimum is 1.78) or CMake (e.g. CMake 3.24.1 will throw CMake errors with boost 1.80)
To find the correct version we will explain on example: boost_1_80_0-msvc-14.3-64.exe:
1_80_0 = Version 1.80
-msvc-14.3 = Toolset v143 for Visual Studio 2022 (https://docs.microsoft.com/en-us/cpp/porting/binary-compat-2015-2017?view=msvc-170)
-64 = 64bit

我当时选了boost的最新的版本 1.84，却没有注意后面msvc版本随便下载了一个，导致和我的visual studio 不匹配，所以编译失败，换成对应的版本后编译通过。
boost版本
![image](https://github.com/elena1205/elena1205.github.io/assets/29435898/84ab3cf0-d4cb-48f2-88df-8d2a60eca442)
msvc版本
![image](https://github.com/elena1205/elena1205.github.io/assets/29435898/d24849b3-601b-4d5a-bf90-d5f825e6541d)

3、打开wow.exe无法登录
wiki中有描述到修改realmlist.swf，但是没有说明realmlist.swf是客户端自带的还是生成的，知乎文档中也没有提及，按照wiki所有步骤执行完成后，没有找到realmlist.swf文件，直接运行wow.exe一直提示connect最后连接失败，最后手动创建了一个realmlist.swf；




