---
title: OpenCV minGW编译
tag: c++
---

链接：

[Clion+Opencv3.2终极配置教程 - 简书 (jianshu.com)](https://www.jianshu.com/p/a825e9bdf283)

## CMAKE代码

```Cmake
# OpenCV
set(OpenCV_DIR "your\\opencv\\path") 
# set(OpenCV_DIR "D:\\software\\opencv\\opencv\\mingw-build")
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
add_executable(TwoSum main.cpp)

target_link_libraries(TwoSum ${OpenCV_LIBS})
```

# LibTorch C++ API使用

## 安装cuda和cudnn

给出教程

[Win10 安裝 CUDA、cuDNN 教學](https://medium.com/ching-i/win10-安裝-cuda-cudnn-教學-c617b3b76deb)

## CMAKE代码

需要执行build文件夹下面的exe文件时，需要将dll文件拷贝过来。由于其过程繁琐，故直接将其写入cmake中，这样就可以在加载cmake时就将需要的dll文件拷贝到build文件夹下。

```cmake
cmake_minimum_required(VERSION 3.22)
project(libtorch_test) # 项目名称

set(CMAKE_CXX_STANDARD 14) # CMAKE版本

# LibTorch
set(CMAKE_PREFIX_PATH "D:\\software\\libtorch 1.11\\libtorch\\share\\cmake\\Torch") # prefix path
find_package(Torch REQUIRED) # 找到Torch
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${TORCH_CXX_FLAGS}")

add_executable(libtorch_test main.cpp) # 添加可执行文件
target_link_libraries(libtorch_test "${TORCH_LIBRARIES}") # 链接库
set_property(TARGET libtorch_test PROPERTY CXX_STANDARD 14)


# copy cuda and cudnn dll files to cmake-build-debug(or release)

# The following code block is suggested to be used on Windows.
# According to https://github.com/pytorch/pytorch/issues/25457,
# the DLLs need to be copied to avoid memory errors.

# add this codeblock at the end.
if (MSVC)
    file(GLOB TORCH_DLLS "${TORCH_INSTALL_PREFIX}/lib/*.dll")
    add_custom_command(TARGET libtorch_test
            POST_BUILD
            COMMAND ${CMAKE_COMMAND} -E copy_if_different
            ${TORCH_DLLS}
            $<TARGET_FILE_DIR:libtorch_test>)
endif (MSVC)
```

## 测试代码

```C++
#include <iostream>
#include <torch/torch.h>

int main() {
    auto x = torch::randn({2, 2});
    x = x.to(torch::kCUDA);
    std::cout << x << std::endl;
}
```

输出：

![image-20220623031618836](https://raw.githubusercontent.com/294coder/blog_img_bed/main/imgs/image-20220623031618836.png)