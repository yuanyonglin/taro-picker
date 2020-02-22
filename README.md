# 基于Taro实现日期和时间在一个组件中完成选择

由于Taro(源于微信)中的picker之支持date/time等的通用选择，而像“今天 10点 30分”这样的更加方便选择的格式需要自行定义，故本项目基于pickerView、pickerViewColumn来自定义了一个选择器用于日期和时间在用一个组件中选择完成。

<img src="https://pan.hongtu.me/img/19ef0a3eb807c61d78532faa35c828ba.png" />

## 简介

大多数的时间选择不需要精确到分钟数的个位数字（例如23分），故本项目默认对当前的时间取到下一个十分（例如20分、30分）

大多数的其他选择器没有调整好类似微信的确认和取消按钮，为了达到基本和微信的选择器体验一致，本项目也实现了确认和取消的按钮，并通过props和父组件交互

组件利用了[moment](http://momentjs.cn/)这个日期处理类库的部分特性来让代码更加简洁和稳定，为了保持小程序包的体积尽量小，组件import了moment-mini这个npm包，该组件与父组件交互主要传输的是moment格式的数据，故再父组件中请也引入moment-mini包来进行解析和操作，如果有特殊需要，您可以使用moment的unix()方法或者format()方法来得到相应格式的数据。

## API

#### onConfirm()

点击确认时触发，传递参数为选择器当前选择的时间(moment格式)

#### onCancel()

点击取消时触发，可被父组件用于触发弹框隐藏之类的操作

#### initial()

组件加载时触发，通知父组件初始化时本组件的时间选择结果(由于初始化为当前时间的下一个整十分，故本操作可把初始化时间直接传给父组件用于展示)

## 更多功能

1.目前初始化的日期选择为最多31天，后续计划可配置改初始化天数

2.日期选择器暂时是三列，分别是日、小时、分钟，如果还需要年和月的请求，就还需要添加相应的列，后续计划做成配置
