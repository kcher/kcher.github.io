---
title: Java注解备忘
date: 2017-12-19 15:12:15
categories: 编程
tags: Java
---

前段时间做了个导出商品的功能，这里写笔记就略微简化一下问题，大概类似于如下的问题：

有一个Engineer类，需要将其实例化并输出到控制台，不要把手机号码打印出来。

这里先把Engineer类的代码贴出来，setter/getter方法这里就省略了。

<!--more-->

```Java
package com.mars.annotation;

public class Engineer {
	
	private Integer id;
	
	private String name;
	
	private Integer age;
	
	private String mobile;
	
	private String email;
	
	public Engineer(){}
	
	public Engineer(Integer id, String name, Integer age, String mobile, String email){
		this.id = id;
		this.name = name;
		this.age = age;
		this.mobile = mobile;
		this.email = email;
	}
	
}

```

换做以前我可能会用if去判断是否是mobile字段，是的话不输出或者用BeanUtils的copyProperties方法将其复制到另一个没有mobile字段的定制类里边去，但这样做显然都不太灵活，下次如果要求不将email字段打印出来就又得改了，所以我决定使用注解来解决这个问题。

下面是注解类Ignore的代码

```Java
package com.mars.annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Inherited;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.FIELD})
@Inherited
public @interface Ignore {

}
```

然后在Engineer类的mobile字段上面加上这个注解。
```Java
@Ignore
private String mobile;
```

其实注解只是一个标记，这里在解析对象的时候会判断这个字段是否有Ignore注解出现，有的话就不对齐进行输出了，那么下次要是要求不输出email字段，我就只需要在email字段上面价格Ignore注解便可以了。
```Java
package com.mars.demo;

import java.lang.reflect.Field;
import java.util.List;

import com.google.common.collect.Lists;
import com.mars.annotation.Engineer;
import com.mars.annotation.Ignore;

public class AnnotationTest {
	
	public static void main(String[] args) throws IllegalArgumentException, IllegalAccessException {
		Engineer e1 = new Engineer(1, "张三", 20, "15989190000", "zhangsan@mars.com");
		Engineer e2 = new Engineer(2, "李四", 21, "15989190001", "lisi@mars.com");
		List<Engineer> list = Lists.newArrayList(e1, e2);
		printer(list);
	}
	
	public static <T> void printer(List<T> list) throws IllegalArgumentException, IllegalAccessException{
		for(T t:list){
			Field[] fields = t.getClass().getDeclaredFields();
			for(int i = 0;i < fields.length; i++){
				Field field = fields[i];
				if(field.isAnnotationPresent(Ignore.class)){
					continue;
				}
				field.setAccessible(true);
				System.out.print(field.get(t) + "\t");
			}
			System.out.print("\n");
		}
	}
}

```
运行一下测试程序看看效果，
运行结果：

```
1	张三	20	zhangsan@mars.com	
2	李四	21	lisi@mars.com	
```
