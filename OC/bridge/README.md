# ARC桥接转换
## __bridge
使用__bridge，可以在不改变所有权的情况下，将对象从Core Foundation框架数据类型转换为Foundation框架数据类型（反之亦然）。

##__bridge_retained
使用__bridge_retained，可以将Foundation框架数据类型对象转换为Core Foundation框架数据类型，并从ARC接管对象的所有权。

##__bridge_transfer
使用__bridge_transfer，可以将Core Foundation框架数据类型对象转换为Foundation框架数据类型对象，并且会将对象的所有权交给ARC管理。

## release
Core Foundation框架用creat, retain, copy创建的数据都需要release。
