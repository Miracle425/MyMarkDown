# 基础项目构建命名

```cmake
cmake_minimum_required(VERSION 3.10)
# 指定了最低版本
project(HelloWorld)
# 项目名
add_executable(目标文件，源文件)
# 生成可执行文件
```

执行命名:`cmake CMakeLists.txt所在路径`
会在当前路径中生成Makefile文件，再执行`make`命令即可生成可执行文件

# set命令

set命令用于设置变量，语法如下：

```cmake
set(<variable> <value>... )
```

使用变量的时候需要加上${}，如下：

```cmake
set(SRC main.cpp)
add_executable(hello ${SRC})
```

设置c++标准

```cmake
set(CMAKE_CXX_STANDARD 11)
```

也可以在执行命名的时候执行标准

```shell
cmake -DCMAKE_CXX_STANDARD=11 .
```

指定文件输出路径

```cmake
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# 相对路径和绝对路径都可以
```

# 搜索路径命名

```cmake
aux_source_directory(<dir> <variable>)
#前者是路径，后者是变量
# 可以是c文件也可以是cpp文件
```

```cmake
file(GLOB/GLOB_RECURSE <variable> <globbing-expressions>)
# GLOB_RECURSE会递归搜索
# 第三个参数是搜索的路径和文件类型，例如*.cpp会搜索所有cpp文件，bin/*.c会搜索bin文件夹下的所有c文件
```

PROJECT_SOURCE_DIR是项目根目录是执行cmake命名的时候后面跟着的路径，也就是CMakeLists.txt所在的文件夹的路径

合并两个变量

```cmake
set(a b c)
# a=b c，把b，c合并到a中
```

CMAKE_CURRENT_SOURCE_DIR是当前CMakeLists.txt所在的文件夹的路径，与PROJECT_SOURCE_DIR相同

# 包含头文件
```cmake
include_directories()
# 指定的是一个文件，默认情况下不指定，会在当前文件夹下搜索，指定后会在指定的文件夹下搜索
```

# 制作库
```cmake
add_library(<name> [STATIC | SHARED | MODULE] source1 [source2 ...])
# 第一个参数是库的名字，第二个参数是库的类型(STATIC是静态库，SHARED是动态库)，第三个参数是源文件
```
指定库的输出路径
```cmake
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
```