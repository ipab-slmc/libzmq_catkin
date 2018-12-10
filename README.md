# libzmq_catkin
Catkin wrapper for [libzmq](https://github.com/zeromq/libzmq) and [cppzmq](https://github.com/zeromq/cppzmq).

- Wraps v4.3.0
- Drafts API enabled

## Usage
Using ``libzmq_catkin``, you can use ZeroMQ like any other catkin package:

```cmake
find_package(catkin REQUIRED COMPONENTS libzmq_catkin)
```

And use the in your C++ files as
```cpp
#include <zmq.hpp>
```