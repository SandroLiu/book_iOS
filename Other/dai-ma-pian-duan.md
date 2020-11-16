# 代码片段

### 单例

```objc
#pragma mark 声明.h
#define singleton_interface(className) +(className*)shared##className;

#pragma mark 实现.m
//\在代码中用于连接宏定义,以实现多行定义
#define singleton_implementation(className) \
static className *_instance;\
+(id)shared##className{\
static dispatch_once_t dispatchOnce;\
dispatch_once(&dispatchOnce, ^{\
_instance=[[self alloc]init];\
});\
return _instance;\
}\
+(id)allocWithZone:(struct _NSZone *)zone{\
static dispatch_once_t dispatchOnce;\
dispatch_once(&dispatchOnce, ^{\
_instance=[super allocWithZone:zone];\
});\
return _instance;\
}

// 初始化
- (instancetype)init {
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        _instance = [super init];
    });
    return _instance;
}  
 
```

## 网络请求

#### 全部请求返回后操作

```swift

       private func commitBtnClick() {    
        
        if selectedImages.count > 0 {
            for image in selectedImages {
                self.uploadImage(image: image)
            }
        }
        
        taskGroup.notify(queue: DispatchQueue.main) 
        {[unowned self] in
        
            self.uploadFeedbackContent(text)
            
        }
        
    }
    
     /// 上传图像
    private func uploadImage(image: UIImage) {
        
        taskGroup.enter()
         
        NetworkManager.shared.upload(methodName: .feedbackPic, params: params, fileItem: item) {[unowned self] (response, error) in
        
            if let result = response {
                let path = result["absoluteUrlPath"]
                selfselectedImagesPath.append(path)
            }
            self.taskGroup.leave()
        
    }
    
```