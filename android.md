# Alpha智能科技事业部 Android 编码规范

### 声明
该文档总结自互联网用于内部Android相关编码规范约束,主要分为两部分:1.Java源代码 , 2.Xml文件.
请务必遵守.


### 第一部分 Java源代码相关

1.包命名  
字母全部小写.  

```
cn.alpha.{部门名称}.{项目名称}.{功能名称}

```
2.Java文件名  
首字母大写,遵循驼峰命名法,命名尽量能够简述内容.  
接口文件请以I字母开头,实现接口文件请以I{文件名}Imp格式.

```java
BaseActivity.java
LoginActivity.java

ILoginServer.java
ILoginServerImp.java

```

3.Java源代码  
 统一使用UTF-8编码格式.
 * 版权声明   
位于文件开始出，采用多行注释风格,首行和尾行空出来.

```java
/***

版权描述

***/

```
 * package 部分  
 独立一行,并且下一行空出.

 * import 部分
 该部分的引入顺序为:   
 1.jdk相关文件  
 2.Android SDK 相关文件  
 3.第三方开源相关文件  
 4.本项目相关文件

 **注:以上顺序之间均空出一行**

 * Class注释  
 位于import之下，Class声明之上.

```java
 /***
 功能描述:
 作者:
 时间:
 版本:
 ==============================================

 修改地方描述:
 修改人:
 时间:
 版本:

 ***/

 ```
 **注 ：  
 创建者 可以不用写修改部分  
 修改者 禁止修改原注释,添加修改消息必须用"=====" 分割 **  

 * Class 部分
   *  类名  
    参照文件命名   
   *  常量    
       字母全部大写,格式:类型\_名称, 多个单词用"_"连接.  
       注：关键常量请给出注释
    ```java
    //最大连接数量
    final int INT_MAX_CONNECTION_COUNTS = 1000 ;
    ```

  * 成员变量   
  以m开头,按照驼峰命名法，并且标明访问修饰符,格式 : m{类型}{说明}.  
  注：关键变量请给出注释

    ```java

    //用户名称显示控件
    private TextView mTextViewUserName;

     ```
  * 成员方法  
   方法名：小写字母开头,按照驼峰命名法，格式 ：{动词}{名称}     
   参数：小写字母开头，按照驼峰命名法,格式 ： {类型}{说明}   
   注释 ：请参照IDE工具填写
    ```java

    /*
     *@param filePath
     *        上传文件本地路径
     *@return true
     *        上传成功
     *         false
     *        上传失败
     **/
     public boolean uploadAvator(File filePath) {


          return true;
       }

    ```
