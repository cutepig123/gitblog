# [做一个modern c++的讲座](https://github.com/cutepig123/gitblog/issues/2)

# 内容简介

讲以前的best practise现在已经不是了，主要包括

- 函数直接返回值，而不需要返回参数。移动语义等。以前的vector里面放sharedptr不需要了，可以通过编写可以移动的变量来做到
- lambda，方便stl alg functional写法
- auto
- design pattern的老套做法的变革，现在更可以非侵入性。要求baseclass的，vs 鸭子类型

# 设计原则

- 封装。object维护内部状态
- 哪个更好，自由函数，成员函数，etc
- 尽量值语义 ，减少 引用语意
- 继承 vs fn object
- prefer enforcement to convention

# concerns

- 函数直接返回值：代码性能不是那么一目了然