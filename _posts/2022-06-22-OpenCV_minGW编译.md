# OpenCV minGW编译

链接：

[Clion+Opencv3.2终极配置教程 - 简书 (jianshu.com)](https://www.jianshu.com/p/a825e9bdf283)

## Cmake代码

```Cmake
# OpenCV
set(OpenCV_DIR "your\\opencv\\path") 
# set(OpenCV_DIR "D:\\software\\opencv\\opencv\\mingw-build")
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
add_executable(TwoSum main.cpp)

target_link_libraries(TwoSum ${OpenCV_LIBS})
```

