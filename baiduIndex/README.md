#### 主要思路

> 通过 python selenium 来模拟鼠标操作，在百度指数趋势图上进行移动，每移动一次，就将该时间点的趋势结果抓取下来。
>
> 2019-2020百度指数进行了一次大改版，目前是v2.0。相比于v1.0，v2.0的爬虫更加容易一些
>
> * 在v1.0中，每次移动鼠标，在图片中能看到指数结果，但是在开发者模式中看到的数据是加密过的，导致我们需要保存图片，并通过图像识别的方式来读取图片上的趋势结果  
                  ![image](https://github.com/liuzf13/crawler/blob/master/images/baiduindex_example.jpg)
>
>   
>
> * 在v2.0中，每次移动鼠标，图片上显示的结果不再被加密，可以直接从后端通过 xpath 的方式读取，因此简单了很多



#### 主要步骤

* 登录百度指数

* 选择省份、城市（目前的代码没用到，但是有对应的函数实现）

* 选择时间段

* 模拟鼠标操作，从左往右，每移动一次鼠标，就通过 xpath 的方式读取图片上的趋势结果（对应代码中的 `moveFocus()`函数）

  * 通过开发者模式的 xpath 获取图片上显示的趋势结果，如下图所示

    ![image](https://github.com/liuzf13/crawler/blob/master/images/baiduindex_xpath.jpg)

  * 鼠标移动的距离为画布宽度（上次爬取的时候是1256，目前是1131，代码中对应部分需要进行修改）除以时间轴天数，画布宽度可以在开发者模式中查看，如下图

    ![image](https://github.com/liuzf13/crawler/blob/master/images/baiduindex_canvas.jpg)
