---
layout:     post
title:      "Java----关键字"
subtitle:   ""
date:       2017-06-15 12:00:00
author:     "lzx"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - java
---


> 本文来自网络查询

# instanceof

> instantceof 判断一个对象是否是某一个类的实例

> 可以使用class equals 判断


	public static void main(String args[]){
		String s=new String("jelo");
		System.out.println(s instanceof String);
		System.out.println(s.getClass().equals(String.class));
	}

# native 
> 用来修饰方法，不能用abstract修饰'

> 一个native method方法可以返回任何java类型，包括非基本类型，而且同样可以进行异常控制。这些方法的实现体可以自制一个异常并且将其抛出，这一点与java的方法非常相似。

>native method的存在并不会对其他类调用这些本地方法产生任何影响，实际上调用这些方法的其他类甚至不知道它所调用的是一个本地方法。JVM将控制调用本地方法的所有细节。

>如果一个含有本地方法的类被继承，子类会继承这个本地方法并且可以用java语言重写这个方法（这个似乎看起来有些奇怪），同样的如果一个本地方法被fianl标识，它被继承后不能被重写。
 如果一个方法描述符内有native，这个描述符块将有一个指向该方法的实现的指针。这些实现在一些DLL文件内，但是它们会被操作系统加载到java程序的地址空间。当一个带有本地方法的类被加载时，其相关的DLL并未被加载，因此指向方法实现的指针并不会被设置。当本地方法被调用之前，这些DLL才会被加载，这是通过调用java.system.loadLibrary()实现的。

# strictfp
> 精确浮点运算

>
strictfp来声明一个 类、接口或者方法时，那么所声明的范围内Java的编译器以及运行环境会完全依照浮点规范IEEE-754来执行。

>
你可以将一个类、接口以及方法声明为strictfp，但是不允许对接口中的方法以及构造函数声明strictfp关键字。

# transient
>
一个对象只要实现了Serilizable接口，这个对象就可以被序列化，Java的这种序列化模式为开发者提供了很多便利，可以不必关系具体序列化的过程，只要这个类实现了Serilizable接口，这个的所有属性和方法都会自动序列化。

> 但是有种情况是有些属性是不需要序列号的，所以就用到这个关键字。只需要实现Serilizable接口，将不需要序列化的属性前添加关键字transient，序列化对象的时候，这个属性就不会序列化到指定的目的地中。

	try {  
          // 序列化，被设置为transient的属性没有被序列化                     
	    ObjectOutputStreamo = new ObjectOutputStream(new FileOutputStream(  
                            "UserInfo.out"));  
                  o.writeObject(userInfo);  
                    o.close();  
         } catch (Exception e) {  
                   e.printStackTrace();  
           }  
            try {  
                    // 重新读取内容  
                    ObjectInputStream in = new ObjectInputStrea( new FileInputStream(  
                                   "UserInfo.out"));  
                     UserInforeadUserInfo = (UserInfo) in.readObject
                         // 读取后psw的内容为null  
                      System. out.println(readUserInfo.toString());  
                } catch (Exception e) {  
                     e.printStackTrace();  
              }  

# volatile

>
用volatile修饰的变量，线程在每次使用变量的时候，都会读取变量修改后的最的值（保证数据的可见性）

>
 长类型的原子性（sun jdk默认已经实现了）


>
在 java 垃圾回收整理一文中，描述了jvm运行时刻内存的分配。其中有一个内存区域是jvm虚拟机栈，每一个线程运行时都有一个线程栈，
线程栈保存了线程运行时候变量值信息。当线程访问某一个对象时候值的时候，首先通过对象的引用找到对应在堆内存的变量的值，然后把堆内存
变量的具体值load到线程本地内存中，建立一个变量副本，之后线程就不再和对象在堆内存变量值有任何关系，而是直接修改副本变量的值，
在修改完之后的某一个时刻（线程退出之前），自动把线程变量副本的值回写到对象在堆中变量。这样在堆中的对象的值就产生变化了。下面一幅图
描述这写交互
![](/img/Java/1.jpeg)


> read and load 从主存复制变量到当前工作内存

> use and assign  执行代码，改变共享变量值 

>
store and write 用工作内存数据刷新主存相关内容

>
其中use and assign 可以多次出现
但是这一些操作并不是原子性，也就是 在read load之后，如果主内存count变量发生修改之后，线程工作内存中的值由于已经加载，不会产生对应的变化，所以计算出来的结果会和预期不一样

>
对于volatile修饰的变量，jvm虚拟机只是保证从主内存加载到线程工作内存的值是最新的
例如假如线程1，线程2 在进行read,load 操作中，发现主内存中count的值都是5，那么都会加载这个最新的值

>
在线程1堆count进行修改之后，会write到主内存中，主内存中的count变量就会变为6
线程2由于已经进行read,load操作，在进行运算之后，也会更新主内存count的变量值为6
导致两个线程及时用volatile关键字修改之后，还是会存在并发的情况。

# Enum 枚举类型

>
	//无参数
	public class TestEnum {
		public enum Hello{
			 Jenny,
			 Tom;
		}
		public static void main(String args[]){
		 	Hello name=Hello.Jenny;
		 	System.out.println(name);
		}
	}

>有参数

	public enum Hello{  '

	        Jenny("Jenny1"),  
	        Tom("Tom1"),  
	        Antia("Antia1"),  
	        Crite("Crite1");  
	        private String name;  
	          
	        Hello(String name){  
	              
	            this.name = name;  
	        }  
	  
	        public String getName() {  
	            return name;  
	        }  
	  
	        public void setName(String name) {  
	            this.name = name;  
	        }  
     }  

# assert
> 
Java2在1.4中新增了一个关键字：assert。在程序开发过程中使用它创建一个断言(assertion)。


> 它的语法形式有如下所示的两种形式：

>> assert condition;
    这里condition是一个必须为真(true)的表达式。如果表达式的结果为true，那么断言为真，并且无任何行动
    如果表达式为false，则断言失败，则会抛出一个AssertionError对象。这个AssertionError继承于Error对象，
    而Error继承于Throwable，Error是和Exception并列的一个错误对象，通常用于表达系统级运行错误。

>> asser condition:expr;
    这里condition是和上面一样的，这个冒号后跟的是一个表达式，通常用于断言失败后的提示信息，说白了，它是一个传到AssertionError构造函数的值，如果断言失败，该值被转化为它对应的字符串，并显示出来。

> 
 Java的assertion却是在运行的时候进行决定的。

>
 assert关键字需要在运行时候显式开启才能生效，否则你的断言就没有任何意义。
