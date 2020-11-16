# TableView优化

## 高度计算优化
1. 后台线程布局
2. 缓存行高

## 控件层级优化
1. 对于不需要点击事件的视图尽量使用CALayer绘制
2. 尽量减少视图的层级
3. 尽量将视图的opaque设置为YES, 避免无用的Alpha通道合成
## 图片显示优化
1. 圆角的使用尽量生成圆角的位图显示，不要使用CALayer的圆角属性
2. 图片的网络加载使用异步加载，进行缓存
3. 图片解码，使用UIImage或CGImageSource创建图片时，图片设置到UIImageView或者CALayer.contents中去，并且CALayer被提交到GPU前，才会解码。最好是先把图片在后台线程绘制到CGBitmapContext中，然后从Bitmap直接创建图片
4. 使用CG开头的方法绘制图像时，最好放到后台线程中。
## Autolayout使用
1. 复杂视图性能会有影响，这时最好使用frame布局方式

## 文本计算
1. 在后台对文本的布局进行计算

## 定时器

## 下载