title: "AOP"
date: 2015-03-11 16:54:35
tags:
---
AOP即面向切面编程。AspectJ是AOP最早成熟的Java实现，它稍微扩展了一下Java语言，增加了一些Keyword:

- Aspect:用来定义切面，该切面可以包含多个切入点和通知，而且标签内部的通知和切入点定义是无序的
- Pointcut:表示一个切入点或触发点，切入点支持的切入点指示符有几种，execution表示执行点，call表示调用点
- execution：使用“execution(方法表达式)”匹配方法执行，方法表达式的格式（注解？ 修饰符? 返回值类型 类型声明?方法名(参数列表) 异常列表？）
- Advice：Pointcut被触发，所产生相应的动作。Advice在AspectJ有三种：before、 after、Around（调用先后均执行）