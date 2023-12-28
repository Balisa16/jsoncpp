# JSON-Thirdparty

Focusing on used for cmake thirdparty in project. And removing unused items in C++ project.
<br>
Forked from [JsonCpp](https://github.com/open-source-parsers/jsoncpp.git) project.

## Install
### Install into local computer library
```
git clone https://github.com/Balisa16/jsoncpp.git
cd jsoncpp && mkdir -p build && cd build
cmake .. && make -j$(( $(nproc) - 1 ))
sudo make install
```
### Used as Thirdpaty project
```
# Go to main project diretory
git submodule add git clone https://github.com/Balisa16/jsoncpp.git thirdparty/jsoncpp
git submodule update --init
```
In cmake add this script
```
add_subdirectory(thirdparty/jsoncpp)
include_directories(thirdparty/jsoncpp/include)

# If used for library
add_library(ADDED_LIBS STATIC
    src/example_lib.cc)
target_link_libraries(ADDED_LIBS PRIVATE jsoncpp)

# if used for executable
add_executable(example_exe localtion/main.cpp)
target_link_libraries(example_exe PRIVATE jsoncpp)
```