# ObfuscatorXcplugin

### xcplugin

解压`Obfuscator-xcplugin`目录内的文件，得到`Obfuscator.xcplugin.zip`   

1.`The Unarchiver`直接解压  
2.使用`cat`命令  

``` 
cat xc* > file.zip
```
打开`file.zip`得到`Obfuscator.xcplugin.zip`  
解压`Obfuscator.xcplugin.zip`得到`Obfuscator.xcplugin`

### 使用  
将`Obfuscator.xcplugin`放入  
`/Applications/Xcode.app/Contents/PlugIns/Xcode3Core.ideplugin/Contents/SharedSupport/Developer/Library/Xcode/Plug-ins/`    

### xcconfig

```
1.New File... 
2.iOS
3.Other
4.Configuration Settings File
```

`Config.xcconfig`内填写  

```
GCC_VERSION = com.apple.compilers.llvm.obfuscator.4_0
COMPILER_INDEX_STORE_ENABLE = NO
OTHER_CFLAGS = -mllvm -bcf -mllvm -fla -mllvm -sub
```

`PROJECT`内`configurations`选择`Config.xcconfig`


### 支持标记  

```
-mllvm -bcf
-mllvm -bcf_loop=1
-mllvm -fla
-mllvm -split 
-mllvm -split_num=1
-mllvm -sub 
-mllvm -sub_loop=1
```

### 指定方法混淆  

`static NSString* method(id param) __attribute((__annotate__(("bcf fla split sub"))));`

### 后续  
插件是通过[obfuscator](https://github.com/obfuscator-llvm/obfuscator)生成的。  
`Hopper Disassembler`打开编译后的二进制查看对比。  
`xcconfig`可以通过`cocoaPods`配置，动态的对核心库，核心代码做混淆。  

### Obfuscator参考  
[obfuscator](https://github.com/obfuscator-llvm/obfuscator)   
[ollvm-in-iOS](http://fighting300.com/2017/09/07/ollvm-in-iOS/)  

# Hikari  

打开`分支hikarich`，按解压步骤获取`Obfuscator.xcplugin-hikarich.zip`，解压后放入  
`/Applications/Xcode.app/Contents/PlugIns/Xcode3Core.ideplugin/Contents/SharedSupport/Developer/Library/Xcode/Plug-ins/`    

`Hikari`目前支持下文所述的编译器标记  

```
-mllvm -enable-bcfobf 启用伪控制流  
-mllvm -enable-cffobf 启用控制流平坦化
-mllvm -enable-splitobf 启用基本块分割  
-mllvm -enable-subobf 启用指令替换  
-mllvm -enable-acdobf 启用反class-dump  
-mllvm -enable-indibran 启用基于寄存器的相对跳转，配合其他加固可以彻底破坏IDA/Hopper的伪代码(俗称F5)  
-mllvm -enable-strcry 启用字符串加密  
-mllvm -enable-funcwra 启用函数封装
```
`-mllvm -enable-allobf`一次性启用前文所述的所有标记。  
注意：不支持指定方法混淆，混淆指令可能会被Release优化。  


### Hikari参考  

[HikariObfuscator](https://github.com/HikariObfuscator/Hikari)  
[Hikari混淆器文档中文版](https://naville.gitbooks.io/hikaricn/content/)  