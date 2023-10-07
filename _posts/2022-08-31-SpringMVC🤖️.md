### `SpringMVC`

#### 一.**MVC**

##### `1.MVC的解释:`

​	🌟MVC模式是一种架构思想
​		1⃣️ M:  Model-模型	 		  指的是模型数据 即数据库的数据
​		2⃣️ V：View-试图 				指的是前端的视图
​		3⃣️ C：Controller-控制器	指的是控制器 用于连接前端视图层和后端的数据层 还有 把后台的数据进行逻辑处理后返回给前端的视图层

##### `2.MVC的优势`

​	1⃣️解除各个模块的耦合度
​	2⃣️便于系统的维护
​	3⃣️便于项目的管理和拓展



#### 二.**MVC的执行流程**

##### `1.前端发起一个Http请求 如果匹配DispatchServlet的请求路径 那么就让DispatchServlet去处理 `

##### `2.DispatchServlet根据对应的请求信息 去HandlerMapping去寻找对应的Handler`

##### `3.得到Handler后对其进行统一封装成HandlerAdapter 再去用同一适配器接口 调用具体的Handler`

##### `4.处理完后会得到一个ModelAndView 返回给DispatchServlet`

##### `5.DispatchServlet会将这个ModelAndView 使用视图解析器去解析 解析完毕后 返回一个View对象`

##### `6.前端页面对View对象进行渲染`

#### 三.**SpringMVC的常用注解**

##### `1.@RequestMapping `-@RequestMapping("comment")

###### 		@GetMapping、@DeleteMapping、@PutMapping、@PostMapping

##### `2.@RestController` 标注为支持Rest风格的控制器层

##### `3.@CrossOrigin` 解决跨域问题

##### `4.@Autowired` 自动注入Spring容器中的类

##### `5.@RequestBody`:表示接收前端的一个对象 并且绑定到控制器的方法参数上

##### `6.@RequestParam` 表示 接收请求路径中传入的参数 并且绑定到控制器的方法参数上

##### `7.@PathVariable` 接收路径中传入的请求参数 restful风格的

#### 四.**拦截器**

##### `1.拦截器会对请求进行拦截处理 `

##### `2.处理逻辑`

​	请求来到 首先通过preHandle()处理 如果为true 则放行到controller层进行逻辑处理 然后到postHandle()方法 然后进行视图解析 最后进入AfterCompletion

##### `3.具体实现`

​	1⃣️一般先定义一个类 xxxxInterper 实现handlerInterper接口 然后实现其preHander()方法、postHander()、afterCompletion()方法
​	一般在preHander方法中 处理拦截信息 如果为true 则放行 为false则抛出异常

​	2⃣️ 然后定义一个 InterceptorConfig类 并且以`@Configuration`注入Spring中 然后写一个方法获取  xxxxInterper类实例 然后重写addInterceptors 把拦截器注册 并且 添加具体拦截到路

##### `4.拦截器和过滤器的具体区别`

​	1⃣️拦截器是基于Spring组件不依赖Tomcat 而过滤器则是Servlet上的应用依赖Tomcat
​	2⃣️拦截器底层基于反射去实现的 而过滤器是基于函数回调实现的
​	3⃣️拦截器实现handlerIntercepetor接口 而过滤器实现javax.servlet
​	4⃣️拦截器拦截的是Contoller层的请求 而过滤器能拦截所有请求
​	5⃣️拦截器在controllor整个生命周期能多次调用 过滤器则只能在容器初始化时候调用
