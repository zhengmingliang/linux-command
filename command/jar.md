jar
===
### 补充说明
进行打包 — 把多个文件打包成一个压缩包 — 这个压缩包和Winzip的压缩格式是一样的.

　区别在于jar压缩的文件默认多一个META-INF的文件夹,该文件夹下包含一个Manifest.mf(清单文件)的文件

　通常来说jar命令得到的压缩包有三种(压缩格式完全一样,只是后缀名不同而已):

　　A、*.jar – 它里面包含N个class文件。

　　B、*.war (web) – 它是一个web应用打包生成的。

　　C、*.ear(Enterprise) -它是一个企业应用打包生成的包

### 用法:
```
 jar {ctxui}[vfmn0PMe] [jar-file] [manifest-file] [entry-point] [-C dir] files ...
```

### 选项:
```
    -c  创建新档案
    -t  列出档案目录
    -x  从档案中提取指定的 (或所有) 文件
    -u  更新现有档案
    -v  在标准输出中生成详细输出
    -f  指定档案文件名
    -m  包含指定清单文件中的清单信息
    -n  创建新档案后执行 Pack200 规范化
    -e  为捆绑到可执行 jar 文件的独立应用程序
        指定应用程序入口点
    -0  仅存储; 不使用任何 ZIP 压缩
    -P  保留文件名中的前导 '/' (绝对路径) 和 ".." (父目录) 组件
    -M  不创建条目的清单文件
    -i  为指定的 jar 文件生成索引信息
    -C  更改为指定的目录并包含以下文件
```
    
如果任何文件为目录, 则对其进行递归处理。
清单文件名, 档案文件名和入口点名称的指定顺序
与 '`m`', '`f`' 和 '`e`' 标记的指定顺序相同。


### 示例
#### 1. 创建压缩包
将两个类文件归档到一个名为 classes.jar 的档案中:
```
jar cvf classes.jar Foo.class Bar.class
``` 
 
#### 2. 使用现有文件清单创建压缩包
 
使用现有的清单文件 'mymanifest' 并
           将 foo/ 目录中的所有文件归档到 'classes.jar' 中: 
```
jar cvfm classes.jar mymanifest -C foo/ .
```


#### 3.创建压缩包，不生成清单文件MANIFEST.MF 
需要大写M
```
jar -cMf mytest.jar *.class
```

### 4. 查看压缩包
```
　jar -tf mytest.jar

　jar -tvf mytest.jar
```

### 5. 解压
```
解压到当前目录
jar -xf mytest.jar

#  解压可看到详细的过程
jar -xvf mytest.jar
```
### 6. 更新压缩包
```
jar -uvf mytest.jar 要加入的指定class文件
```

### 7. 打包成可执行jar包
通过 -e 选项 告诉系统哪个类是该jar包的主类
```
# 打包
jar -cvfe mytest.jar UserTest *.class(指定的主类)

# 执行
java -jar mytest.jar

```