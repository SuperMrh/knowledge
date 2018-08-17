## RESTful  API

~~~python
'''
注：本次项目基于Python，用到的框架是Django
RESTful --> 表象性状态转移风格
重要的概念： 面向资源编程（资源 --> 一类数据） 
		最重要不是面向资源的概念，而是如何去表述一个资源 --> 地址即资源
例子：
	http://api.demo.com/users --> 所有的用户
    http://api.demo.com/users/1/articles --> ID为1的用户的所有文章

前后分离后，项目的开发重心发生了变化。前后分离之前，项目主要侧重于后端。后端对数据进行处理，
并返回响应的数据，然后前端部分的只需要拿取到返回的数据，并在页面上进行渲染就可以了。而前后分
离之后，后端开发人员需要做的仅仅是写相应的接口，处理数据，返回相应的JSON数据，前端人员通过动
态请求（ajax）接口，获取数据，然后动态生成网页内容。
'''
~~~

#### 前后分离之前 - 后端处理

~~~python
# 后端按照前端的需求去数据库请求数据，然后将数据返回给前端页面。
~~~



![1534205359737](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534205359737.png)

#### 前后分离之前 - 前端处理

~~~python
# 前端页面接收到数据后，通过模板语法去解析数据，渲染网页内容。
~~~



![1534207928959](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534207928959.png)

#### 前后分离后初级 - 后端处理

~~~python
'''
前后分离之后，使用JsonResponse()的时候无法返回一个对象给前端（JsonResponse()无法序列化对
象）。这样前端就无法取到一个对象，然后对对象进行解析，无法比较方便快捷的取到想要的数据，这时
候前端需要获取一些特定的数据的时候就需要在JS里面编写一个ajax请求来请求后端的相应接口，获取
指定的数据。形式如下图所示:
'''
~~~

![1534206073308](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534206073308.png)

#### 前后分离后初级 - 前端处理

![1534208167404](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534208167404.png)

#### 前后分离进阶

~~~python
'''
上面的开发模式完成了前后端的分离开发，后端负责数据接口的开发，然后前端去请求接口，获取相应的
数据，然后通过JS动态生成页面内容。但如果只是仅仅这样的话，也会有一些不期望的问题出现，那就是
项目越大，涉及到的数据请求就会越多，那么后端需要提供的接口就越多，而当接口数量到达一定的程度
的时候，难免不会写出重复的接口，而且在后续代码维护或更新版本的时候，可能不是由同一个人进行，
那么这种情况下，开发人员无疑会浪费很多的时间在理解接口上面。
要避免这种情况，一个清晰明了的接口文档往往会在一定程度上解决这个问题，但从根本上去解决，我们
可能需要尽可能的减少接口数量。而这种情况，设计一套符合规范的RESTful风格的接口就能够帮我们很
好的实现。
'''
~~~

#### 实现一个最基本的RESTful接口

~~~python
'''
(1): 导入相关模块 / 在工程url中注册rest_framework
(2): 定义序列化模型(serializer) --> 依靠Serialiers将数据库取出的数据Parse为API的数据
(3): 实例化SimpleRouter对象 / 注册需要管理的资源和处理视图函数
(4): 定义用户资源模型
'''
~~~

####(1)导入相关模块 / 在工程url中注册rest_framework

![1534291903320](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534291903320.png)

####(2)定义序列化模型(serializer)

~~~python
# 元类指定关联模型和指定序列化的字段
~~~



![1534291984168](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534291984168.png)

#### (3)实例化SimpleRouter对象 / 注册需要管理的资源和处理视图函数

![1534292347422](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534292305798.png)

####(4)定义用户资源模型

~~~python
'''
mixins.ListModelMixin --> List a queryset.(展示一个查询集合里面的所有内容)
mixins.RetrieveModelMixin --> Retrieve a model instance.(检索模型实例,需要参数id)
mixins.CreateModelMixin --> Create a model instance.(创建模型实例)
mixins.DestroyModelMixin --> Destroy a model instance.(删除模型实例)
mixins.UpdateModelMixin --> Update a model instance.(更新模型实例)
'''
~~~



![1534292418000](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534292418000.png)

#### 前端的AJAX请求及响应

![1534292518974](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534292518974.png)

![1534464533454](https://github.com/SuperMrh/knowledge/blob/master/rest_images/1534292680512.png)

~~~python
'''
上述接口返回了所有的用户的相关信息。这个接口还允许其他的请求方式(POST,PUT,PATCH等)。那些跟
项目模型信息相关的数据操作（增/删/改/查）都可以通过请求这一类的接口去进行。这样就大大减少了
接口的数量，更易于管理维护。
了解相关内容的可以查看Django REST框架官方文档：http://www.django-rest-framework.org/
'''
~~~

