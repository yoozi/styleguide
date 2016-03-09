# Alpha智能科技事业部 Android 编码规范

### 声明
该文档总结自互联网用于内部Android相关编码规范约束.  
主要分为两部分:1.Java源代码 , 2.Xml文件.  
请务必遵守.  
如有不合适的地方望指正。


### 第一部分 Java源代码相关

1.包命名  
字母全部小写.  

```
cn.alpha.{部门名称}.{项目名称}.{功能名称}

```
2.Java文件名  
首字母大写,遵循驼峰命名法,命名尽量能够简述内容.
接口文件请以 I 字母开头,实现接口文件请以 I{文件名}Imp 格式.

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
    
    
* Class注释  
 位于import之下，Class声明之上. 

 ```
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
 
 修改者 禁止修改原注释,添加修改消息必须用"=====" 分割  

* Class 部分
   *  类名  
    参照文件命名   
   *  常量    
       字母全部大写,格式:{类型}\_{名称}\_{简述}, 多个单词用"_"连接.  
       注：关键常量请给出注释
      
    ```java  
    
    
    //最大连接数量
    final int INT_MAX_CONNECTION_COUNTS = 1000 ;
    
    ```

  * 成员变量   
  以m开头,按照驼峰命名法，并且标明访问修饰符,格式 : m{类型}{简述}.  
  注：关键变量请给出注释  
  
    ```java

    //用户名称显示控件
    private TextView mTextViewUserName;

    ``` 
     
     
  * 成员方法  
   方法名：小写字母开头,按照驼峰命名法，格式 ：{动词}{操作对象名称}     
   参数：小写字母开头，按照驼峰命名法,格式 ： {类型}{简述}   
   注释 ：请参照IDE工具填写  
   
    ```java

    /*
     * 功能性简述
     * 功能性详述
     * 
     *@param filePath
     *        上传文件本地路径
     *@return true
     *        上传成功
     *         false
     *        上传失败
     **/
     public boolean uploadAvator(String filePath) {


          return false;
       }

    ```  
  
  * 其他  
    针对继承至Android四大组件的Class代码排列顺序，必须按照其对应的生命周期进行排列并位于Class开始位置，其后为自定义方法.  
    注： 可以使用IDE插件排序.
  
* 其他部分
  * import 禁止用 [*] 进行通配.
  * 代码行缩进 用 [TAB].
  * 独立一行代码 也需要用 [{ }]括起来,特别是for，if 等.
  * switch语句中，必须包含default语句
  * 代码列宽是80或100个字符
  * 运算符前后均留一个[空格]
  
### 第二部分 Xml代码相关
命名统一采用小写字母,多个单词之间用 [_] 连接.

 * 布局文件  
   
   * 文件名   
      格式 ： layout\_{使用的组件类别}\_{使用的Class名称的内容单词}.xml
   * 控件id   
      格式 ：{2个以上单词取每个单词首字母 | 一个单词取开头3个字母}_{代表的内容名称}
      
   ```   
   layout_activtiy_login.xml  
   item_listview_contacts.xml
   ```
   
       ```xml
    
    <ImageView
        android:id="@+id/iv_avator"
        android:layout_width="250dp"
        android:layout_height="250dp"
        android:background="@drawable/shape_bg_iv_avator"
        />
    <Button
        android:id="@+id/but_login"
        android:layout_width="match_parent"
        android:layout_height="200dp"
        android:text="Login"
        />
   
       ```
     
 * Drawable文件
   * xml文件名  
     格式 ： {文件内容类型}\_{使用的地方}_{控件id}.xml
     
      ```
      shape_bg_iv_avator.xml
      selector_bg_but_login.xml
      ```  
   
   * 图片文件名  
     格式 ： {使用的地方}\_{控件id}\_{其他}.jpg/png 
      
     ```
     bg_but_login_focused.png/jpg
     ```
     
     
 * Values 文件  
   资源属性名称：多单词组合 并用"_"连接.  
   格式 ：{简述1}\_{简述2}
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="primary">#3F51B5</color>
    <color name="primary_dark">#303F9F</color>
    <color name="accent">#FF4081</color>
</resources>
   ```
   
   ```
   <resources>
    <string name="app_name">AnniationDemo</string>
    </resources>
   ```  
   
   ``` 
   <resources>
    <dimen name="activity_horizontal_margin">16dp</dimen>
    <dimen name="activity_vertical_margin">16dp</dimen>
    
    
    <dimen name="front_size_big">18sp</dimen>
    <dimen name="front_size_middle">14sp</dimen>
    <dimen name="front_size_small">12sp</dimen>
</resources>
   ```
   
    
