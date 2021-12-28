[TOC]



# 安装

![image-20210305005112931](image/image-20210305005112931.png)

我们把集成方案和基础模板下载下来，

template是集成了核心的必须的功能，我们可以在template上进行二次开发，开发过程中可以将admin中参照admin来对template进行功能上的添加



然后进入到template目录中进行依赖的安装

![image-20210305005708304](image/image-20210305005708304.png)





然后我们让这个项目跑起来

![image-20210305005845708](image/image-20210305005845708.png)

![image-20210305005858602](image/image-20210305005858602.png)

然后这个项目就成功跑起来了









# easy-mock

就是用来提供前端进行接口访问的假数据

![image-20210305010438567](image/image-20210305010438567.png)

easymock的官网突然就崩了，然后自己部署也失败，所以先用着fast mock凑合一下吧





![image-20210305015959529](image/image-20210305015959529.png)

注册登录之后，我们在上面创建一个项目

![image-20210305020038985](image/image-20210305020038985.png)

点进去

![image-20210305020221721](image/image-20210305020221721.png)

新建一个接口



![image-20210305020746736](image/image-20210305020746736.png)





点击保存，假数据接口就做好了







# 目录结构介绍







# 分页



## 什么是假分页和真分页

![image-20210312020214063](image/image-20210312020214063.png)

> 总结就是真分页是点击一次分页按钮就向服务器请求一次，获取部分的数据（适合数据库数据量大的情况）
>
> 假分页就是一次性获取所有数据，然后前台对数据进行分页（适合数据库数据量小的情况）





通过在官网查询分页，可以看到

![image-20210312000715379](image/image-20210312000715379.png)



然后我们打开admin项目，找到在综合表格中，找到pagination



![image-20210312000818874](image/image-20210312000818874.png)

可以看到，pagination这个组件在components文件夹下，然后我们找到这个组件

![image-20210312000855004](image/image-20210312000855004.png)

就可以跟着官网的教程来学习了



然后我们配置mybatis plus的分页查询，使用的是mybatis plus的分页插件，如果是使用的mybatis 可以使用pagehelper分页插件（关于pagehelper的教程可以看我学习vue-element-admin的教程）



## selectPage

分页查询

![image-20210312013144467](image/image-20210312013144467.png)

![image-20201226140642111](image/image-20201226140642111.png)



如果我们想要查询出第二页，只需要修改为2就可以了’

![image-20201226140716335](image/image-20201226140716335.png)







## 多表查询+分页操作

一样的添加好mybatisplusconfig的分页插件之后

我们将两个表合并成一个实体类

![image-20210409225659119](image/image-20210409225659119.png)

然后编写mapper

![image-20210410014831212](image/image-20210410014831212.png)

编写service

![image-20210410014917995](image/image-20210410014917995.png)

编写测试类就完成了

![image-20210410014940536](image/image-20210410014940536.png)

![image-20210410014947526](image/image-20210410014947526.png)



















**关于没有分页效果的问题**

这是因为我们没有在配置类中添加分页的插件

**使用selectpage之前要添加这个分页的插件**

<img src="image/image-20201226140554194.png" alt="image-20201226140554194" style="zoom:80%;" />







我们的spring boot项目添加了分页插件之后，然后我们就可以创建controller和service层的方法了

![image-20210312043744091](image/image-20210312043744091.png)

![image-20210312043732357](image/image-20210312043732357.png)

通过前端的postman来对接口进行测试

![image-20210312020031446](image/image-20210312020031446.png)

>  如上，获取第二页，没页8条数据



在这里，我们的后台分页接口就完成了，现在就可以开始前台分页的代码构造了



- 通过admin中，我们将admin的代码移植到我们的项目

![image-20210312032749563](image/image-20210312032749563.png)

因为pagination依赖于utils中的scroll-to

![image-20210312032831427](image/image-20210312032831427.png)

所以我们导入



然后在我们要修改的表的组件中，添加

![image-20210312032900567](image/image-20210312032900567.png)

![image-20210312032914562](image/image-20210312032914562.png)



然后在组件的data中设置分页组件的参数

![image-20210312033040412](image/image-20210312033040412.png)

![image-20210312033641580](image/image-20210312033641580.png)



然后我们table的数据也要来自于分页查询的数据

![image-20210312044628767](image/image-20210312044628767.png)

![image-20210312044642319](image/image-20210312044642319.png)

> 这样就完成了，我们不需要自己修改listquery.page的值，当我们点击这个按钮的时候，pagination会动态帮我们修改

![nignationdemo01](image/nignationdemo01.gif)



## 关于我们没有设置点击分页跳转，但是能自动实现listquery.page的参数自动改变

我们看看其源码



![image-20210312045754351](image/image-20210312045754351.png)

其实就是这两个事件在帮我们完成的，具体有空看源代码吧，其实关于其他的背景色之类的也可以通过查看源代码来自行修改



# 修改当前element的语言

![image-20210312045252706](image/image-20210312045252706.png)

![image-20210312045321783](image/image-20210312045321783.png)











# 微信支付









# 控制element ui 表格的显示

比如如果这个对象的信息被标记被已删除，那么我们就把这个对象过滤掉

我们先获取数据列表

![image-20210410165700797](image/image-20210410165700797.png)

然后我们把这个计算模板放在element ui表格的数据model就行了

![image-20210410165739903](image/image-20210410165739903.png)

![image-20210410165805103](image/image-20210410165805103.png)

这样就不会显示已删除的用户信息





# 可能出现的问题

## axios post请求 vue-element-admin 接口请求等很久，最后报400错误

记得要重启webpack项目，热部署是不生效的

建议使用第二种方式

**第一种方法**（不建议使用）



![blog.csdn.net_weixin_44896595_article_details_115088342](image/blog.csdn.net_weixin_44896595_article_details_115088342.png)



**第二种方法**



原本该文件的代码如下

![image-20210410150530666](image/image-20210410150530666.png)

![image-20210410150537425](image/image-20210410150537425.png)

修改后如下



![blog.csdn.net_Seven71111_article_details_107852984](image/blog.csdn.net_Seven71111_article_details_107852984.png)

**上面的两种方法都需要重新部署项目**