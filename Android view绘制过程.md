#### Measure、Layout、Draw三个主要的过程

#### Measure是对View大小测量

#### 自定义View
```
覆写onMeasure方法,计算合适的大小,并将结果通过setMeasuredDimension()方法保存结果
```
#### 自定义ViewGroup
```
除了完成View的自定义过程,还要调用View的measure方法,确保每个子View都正确的测量
```
