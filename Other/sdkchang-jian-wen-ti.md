# SDK常见问题

### SDK添加测试target 编译报错（_main）
- 这是因为SDK编译的是静态库
- 选择测试target-> build Settings -> Mach-o Type -> Bundle 