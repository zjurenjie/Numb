# cmake教程
## 基本语法规则
1. 变量使用${}取值，IF控制语句中直接使用变量名取值。
2. 指令（参数1 参数2 ...），参数使用括号括起，参数之间使用空格或分号隔开。
3. 指令是大小写无关的，参数是大小写相关的。
4. 需要为任何一个子目录建立一个CMakeLists.txt文件
5. 合法特例
ADD_EXECUTABLE(MAIN "main.c")
ADD_ECECUTABLE(MAIN "fu nc.c")
ADD_EXECUTABLE(MAIN main) //自动寻找main、main.c和main.cpp等文件，不推荐

### PROJECT指令---定义工程名称与类型
```cmake
//TODO：用法
PROJECT(projectname[CXX][C][Java])
//TODO:四个变量
<projectname>_BINARY_DIR = PROJECT_BINARY_DIR //编译路径
<projectname>_SOURCE_DIR = PROJECT_SOURCE_DIR //工程路径
```  
### SET指令---显式的定义变量
```cmake
//TODO:用法
SET(VAR [VALUE][CACHE TYPE DOCSTRING [FORCE]])
//TODO:示例
SET(SRC_LIST main.c a.c b.c c.c)
```  
### MESSAGE指令---向终端输出信息  
```cmake
//TODO:用法
MESSAGE([SNED_ERROR | STATUS | FATAL_ERROR] "message to display")
```  
### ADD_EXECUTABLE---指定生成可执行文件
```cmake
//TODO:用法
ADD_EXECUTABLE(HELLO ${SRC_LIST})
```
### ADD_SUBDIRECTORY---添加源文件子目录，并制定中间二进制与目标二进制的存放位置
```cmake
//TODO:用法
ADD_SUBDIRECTORY(sourece_dir [binary_dir] [EXCLUDE_FROM_ALL]) //EXCLUDE_FROM_ALL 将这个目录剔除
//TODO:示例
ADD_SUBDIRECTORY(src bin) // 将src添加编译目录，制定二进制到bin
```

