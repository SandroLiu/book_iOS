# 常见问题

### Warning: The Copy Bundle Resources build phase contains this target's Info.plist file 'Info

这是由于在Copy Bundle Resources（TARGETS->build phase）中添加了info.plist造成，去掉就可以解决。


### warning: directory not found for option
1. directory not found for option '-L/... 这表示是查询 Library 的时候出现的异常
  
    依次 Project -> targets -> Build Setting -> Library Search Paths删除里面的路径
  
2. directory not found for option '-F/... 这表示是查询 Framework 的时候出现的异常
    
    依次 Project -> targets -> Build Setting -> Framework Search Paths删除里面的路径

### Multiple commands produce Target '' has create directory command with output 
 - 创建路径问题
 - target -> build Phases -> Copy Pods Resources -> 删除Output files内容
 
 #### library not found 
 - build setting 中 library Path 路径不对
 - 模拟器下cocoapods 没有将库打包成.a 文件，设置工程的Build Active Architecture Only
 
 #### DEBUG宏不起作用
 - 设置 build setting 中的 Preprocessor Macros ，设置Debug版为 DEBUG = 1