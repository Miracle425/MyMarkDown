# ADC学习笔记

![alt text](../.images/adc/image.png)

## 18个通道

1. ADCx_IN0~ADCx_IN15

2. 温度传感器

3. VREFINT(内部参考电压)

## injected channel 和 regular channel

injected channel最多可以选择4个通道,regular channel最多可以选择16个通道

但是injected channel对应有4个寄存器,***regular有1个寄存器***,***有存在数据覆盖的可能***,一般来用DMA进行配合

一般情况下用injected channel即可

## 触发方式

1. 软件触发
2. 硬件触发

定时器可以通向ADC和DAC,触发转换

![alt text](../.images/adc/image-1.png)

***将TIM3的更新事件选择为TRGO输出,ADC的开始触发信号选择为TIM3的TRGO,这样TIM3的更新事件就能通过硬件自动触发ADC的转换了,节省了中断资源***

也可以选择外部引脚触发

## 参考电压

![alt text](../.images/adc/image-2.png)

芯片内部中已经连接了

## ADCCLK

![](../.images/adc/image-3.png)

![alt text](../.images/adc/image-4.png)

ADCCLK来自于APB2上,经过ADC预分频器分频成为ADCCLK

最大为14MHz
只能选择6分频 12MHz
只能选择8分频 9MHz

## 一次转换完成处理

![alt text](../.images/adc/image-5.png)

在模拟开门狗检测到通道超过阈值范围,注入通道(JEOC),规则通道(EOC)转换完成后,都会将状态寄存器中置标志位,也可以去NVIC申请中断,如果开启了NVIC对应的通道,他们就可以触发中断

## 基本结构图

![alt text](../.images/adc/image-6.png)

## ADC通道和引脚复用的关系

![alt text](../.images/adc/image-7.png)

![alt text](../.images/adc/image-8.png)

上图ADC12_IN0代表ADC1_IN0和ADC2_IN0

ADC1和ADC2对应的引脚完全相同,ADC3则有些不同

ADC1和ADC2可以进行交叉采样,即对一个通道交叉进行采样,(类似于打拳左打一拳右打一圈)提高采样频率

## 转换模式

***单次转换 连续转换***

***非扫描模式*** ***扫描模式***

两两组合共构成四种模式

1. 单次转换,非扫描模式

![alt text](../.images/adc/image-10.png)

***只有一个通道,启动一次转换一次***

2. 连续转换,非扫描模式

![alt text](../.images/adc/image-11.png)

***只有一个通道,启动一次一直转换下去***

3. 单次转换,扫描模式

![alt text](../.images/adc/image-12.png)

***可以指定通道数目(前n个通道),依次转换前n个通道,为了防止数据覆盖,需要使用DMA,启动依次转换依次***

4. 连续转换,扫描模式
同上

## 触发控制

![alt text](../.images/adc/image-13.png)

## 数据对齐

![alt text](../.images/adc/image-14.png)

ADC的数据是12位 但是数据寄存器是16位的

一般都用右对齐

左对齐会比原来的数大16倍,用途为:取出高八位,舍弃后四位,降低了精度,用于判断与某个值的大小,在精度要求不高的情况下

## AD转换时间(转换步骤)

![alt text](../.images/adc/image-15.png)

***采样保持:打开采样开关,收集电压,再断开采样开关,避免连续变化的电压使得无法正常采样***

***量化编码:逐次比较求结果的过程***

***采样时间:采样保持时间***

ADC周期多半个的原因:干其他事情(具体什么也不知道)

## 校准

![alt text](../.images/adc/image-16.png)

## 硬件电路

![alt text](../.images/adc/image-17.png)

PA1/2/3 接AD转换器

1. PR1是电位器(旋钮式的滑动变阻器)
2. N1是光敏电阻,热敏电阻之类的
3. 将0~5V转换为0~3.3V的方法(10V同理,电压更高时使用专门的转压芯片)

## ADC状态寄存器(ADC_SR ADC Status Register)

![alt text](../.images/adc/image-18.png)

## ADC控制寄存器1(ADC_CR1)

![alt text](../.images/adc/image-19.png)

![alt text](../.images/adc/image-20.png)

![alt text](../.images/adc/image-21.png)

![alt text](../.images/adc/image-22.png)

## ADC控制寄存器1(ADC_CR2,软件触发控制)

![alt text](../.images/adc/image-23.png)

![alt text](../.images/adc/image-24.png)

![alt text](../.images/adc/image-25.png)

![alt text](../.images/adc/image-26.png)

![alt text](../.images/adc/image-27.png)

![alt text](../.images/adc/image-28.png)
