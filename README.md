# libzmq_catkin
Catkin wrapper for [libzmq](https://github.com/zeromq/libzmq) and [cppzmq](https://github.com/zeromq/cppzmq).

- Wraps v4.3.0
- Drafts API enabled

## Usage

Before including any other catkin package, run:

```cmake

find_package(catkin REQUIRED COMPONENTS libzmq_catkin)
set(libzmq_INCLUDE_DIRS "${catkin_INCLUDE_DIRS}/libzmq_catkin")
set(libzmq_LIBRARIES "${catkin_LIBRARIES}")

find_package(catkin REQUIRED COMPONENTS all_your_other_packages)
```
