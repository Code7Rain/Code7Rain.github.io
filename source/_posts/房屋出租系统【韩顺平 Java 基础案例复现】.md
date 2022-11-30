---
title: 房屋出租系统【韩顺平 Java 基础案例复现】
date: 2022-03-24 15:31:36
categories: 项目梳理
tags:
- Java
- 韩顺平
- 项目实战
sticky: 
pic:
comments: true
toc: true
expire: true
only:
- home
- category
- tag
top_img: 
cover: 
---

本项目是根据B站韩顺平【零基础快速 Java】课程进行的。项目的主要目的是学习巩固 Java 基础知识。<!-- more -->

# 房屋出租系统【韩顺平 Java 基础案例复现】

## 前言
本项目是根据B站韩顺平【零基础快速 Java】课程进行的。项目的主要目的是学习巩固 Java 基础知识。

## 一、需求
实现房屋出租系统，基本功能包括对房屋信息的增删改查（存储用数组实现）。

## 二、项目设计-程序框架图
![程序框架图](https://img2022.cnblogs.com/blog/2291368/202202/2291368-20220227144414328-1953458094.png)

## 三、项目代码实现

### 3-1 文件夹结构

![](https://img2022.cnblogs.com/blog/2291368/202202/2291368-20220227160905796-630586732.png)


### 3-2 工具类准备

这里的 Utility 类是韩顺平Utility工具类(java房屋出租项目)，创建工具类文件复制到自己的项目里即可。

```java
package com.codedog.houserent.utils;    //改为自己的目录


/**
	工具类的作用:
	处理各种情况的用户输入，并且能够按照程序员的需求，得到用户的控制台输入。
*/

import java.util.*;

public class Utility {
	//静态属性。。。
    private static Scanner scanner = new Scanner(System.in);

    
    /**
     * 功能：读取键盘输入的一个菜单选项，值：1——5的范围
     * @return 1——5
     */
	public static char readMenuSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1, false);//包含一个字符的字符串
            c = str.charAt(0);//将字符串转换成字符char类型
            if (c != '1' && c != '2' && 
                c != '3' && c != '4' && c != '5') {
                System.out.print("选择错误，请重新输入：");
            } else break;
        }
        return c;
    }

	/**
	 * 功能：读取键盘输入的一个字符
	 * @return 一个字符
	 */
    public static char readChar() {
        String str = readKeyBoard(1, false);//就是一个字符
        return str.charAt(0);
    }
    /**
     * 功能：读取键盘输入的一个字符，如果直接按回车，则返回指定的默认值；否则返回输入的那个字符
     * @param defaultValue 指定的默认值
     * @return 默认值或输入的字符
     */
    
    public static char readChar(char defaultValue) {
        String str = readKeyBoard(1, true);//要么是空字符串，要么是一个字符
        return (str.length() == 0) ? defaultValue : str.charAt(0);
    }
	
    /**
     * 功能：读取键盘输入的整型，长度小于10位
     * @return 整数
     */
    public static int readInt() {
        int n;
        for (; ; ) {
            String str = readKeyBoard(10, false);//一个整数，长度<=10位
            try {
                n = Integer.parseInt(str);//将字符串转换成整数
                break;
            } catch (NumberFormatException e) {
                System.out.print("数字输入错误，请重新输入：");
            }
        }
        return n;
    }
    /**
     * 功能：读取键盘输入的 整数或默认值，如果直接回车，则返回默认值，否则返回输入的整数
     * @param defaultValue 指定的默认值
     * @return 整数或默认值
     */
    public static int readInt(int defaultValue) {
        int n;
        for (; ; ) {
            String str = readKeyBoard(10, true);
            if (str.equals("")) {
                return defaultValue;
            }
			
			//异常处理...
            try {
                n = Integer.parseInt(str);
                break;
            } catch (NumberFormatException e) {
                System.out.print("数字输入错误，请重新输入：");
            }
        }
        return n;
    }

    /**
     * 功能：读取键盘输入的指定长度的字符串
     * @param limit 限制的长度
     * @return 指定长度的字符串
     */

    public static String readString(int limit) {
        return readKeyBoard(limit, false);
    }

    /**
     * 功能：读取键盘输入的指定长度的字符串或默认值，如果直接回车，返回默认值，否则返回字符串
     * @param limit 限制的长度
     * @param defaultValue 指定的默认值
     * @return 指定长度的字符串
     */
	
    public static String readString(int limit, String defaultValue) {
        String str = readKeyBoard(limit, true);
        return str.equals("")? defaultValue : str;
    }


	/**
	 * 功能：读取键盘输入的确认选项，Y或N
	 * 将小的功能，封装到一个方法中.
	 * @return Y或N
	 */
    public static char readConfirmSelection() {
        System.out.println("请输入你的选择(Y/N): 请小心选择");
        char c;
        for (; ; ) {//无限循环
        	//在这里，将接受到字符，转成了大写字母
        	//y => Y n=>N
            String str = readKeyBoard(1, false).toUpperCase();
            c = str.charAt(0);
            if (c == 'Y' || c == 'N') {
                break;
            } else {
                System.out.print("选择错误，请重新输入：");
            }
        }
        return c;
    }

    /**
     * 功能： 读取一个字符串
     * @param limit 读取的长度
     * @param blankReturn 如果为true ,表示 可以读空字符串。 
     * 					  如果为false表示 不能读空字符串。
     * 			
	 *	如果输入为空，或者输入大于limit的长度，就会提示重新输入。
     * @return
     */
    private static String readKeyBoard(int limit, boolean blankReturn) {
        
		//定义了字符串
		String line = "";

		//scanner.hasNextLine() 判断有没有下一行
        while (scanner.hasNextLine()) {
            line = scanner.nextLine();//读取这一行
           
			//如果line.length=0, 即用户没有输入任何内容，直接回车
			if (line.length() == 0) {
                if (blankReturn) return line;//如果blankReturn=true,可以返回空串
                else continue; //如果blankReturn=false,不接受空串，必须输入内容
            }

			//如果用户输入的内容大于了 limit，就提示重写输入  
			//如果用户如的内容 >0 <= limit ,我就接受
            if (line.length() < 1 || line.length() > limit) {
                System.out.print("输入长度（不能大于" + limit + "）错误，请重新输入：");
                continue;
            }
            break;
        }

        return line;
    }
}
```

### 3-3 具体功能类

#### 3-3-1 House类

House实体类的属性有编号，房主， 电话，地址，月租，状态。House的对象表示一个房屋信息。其中构造器、Get和Set方法、toSring方法快捷键Alt+Insert生成即可，toSring略微改成自己想要的格式。

```java
package com.coderq.houserent.domain;

/**
 * Created by Q on 2022/2/26.
 * House对象表示一个房屋信息
 */
public class House {
    //编号  房主  电话  地址  月租  状态（未出租/已出租）
    private int id;
    private String name;
    private String phone;
    private String address;
    private int rent;
    private  String state;

    public House(int id, String name, String phone, String address, int rent, String state) {
        this.id = id;
        this.name = name;
        this.phone = phone;
        this.address = address;
        this.rent = rent;
        this.state = state;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public int getRent() {
        return rent;
    }

    public void setRent(int rent) {
        this.rent = rent;
    }

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }

    //为了方便输出对象信息。实现toString方法
    @Override
    public String toString() {
        //改为想要的格式
        // 编号  房主  电话  地址  月租  状态（未出租/已出租）
        return  id +
                "\t\t" + name +
                "\t" + phone +
                "\t\t" + address +
                "\t\t" + rent +
                "\t\t" + state ;
    }
}
```

#### 3-3-2 HouseView类 

HouseView类用于显示界面

```java 
package com.coderq.houserent.view;

import com.coderq.houserent.domain.House;
import com.coderq.houserent.service.HouseService;
import com.coderq.houserent.utils.Utility;

/**
 * Created by Q on 2022/2/26.
 * <p>
 * 1.显示界面
 * 2.接收用户的输入
 * 3.调用HouseService完成对房屋信息的各种操作
 */
public class HouseView {
    private boolean loop = true;  //控制显示菜单
    private char key = ' ';  //接收用户输入
    private HouseService houseService = new HouseService(10); //设置数组大小为10

    //根据修改房屋信息
    public void updateHouse() {
        System.out.println("=================修改房屋==================");
        System.out.print("请输入待修改房屋id(-1退出查找)");
        int updateId = Utility.readInt();
        if (updateId == -1) {
            System.out.println("=================已退出修改房屋==================");
            return;
        }

        //注意点：
        //返回的是引用类型[即就是数组的元素]，都指向同一对象
        //因此用House.SetXX()方法会修改HouseService中的houses数组中的元素
        House house = houseService.findById(updateId);
        if (house == null) {
            System.out.println("==============修改的房屋信息不存在===============");
            return;
        }
        System.out.println("姓名（" + house.getName() + "）：");
        String name = Utility.readString(8, "");
        if ( !"".equals(name) ) { //修改
            house.setName(name);
        }
        System.out.println("电话（" + house.getPhone() + "）：");
        String phone = Utility.readString(12,"");
        if ( !"".equals(phone) ) { //修改
            house.setPhone(phone);
        }
        System.out.println("地址（" + house.getAddress() + "）：");
        String address = Utility.readString(16,"");
        if ( !"".equals(address) ) { //修改
            house.setAddress(address);
        }
        System.out.println("月租（" + house.getRent() + "）：");
        int rent = Utility.readInt(-1);
        if ( rent != -1 ) { //修改
            house.setRent(rent);
        }
        System.out.println("状态（" + house.getState() + "）：");
        String state = Utility.readString(3,"");
        if ( !"".equals(state) ) { //修改
            house.setState(state);
        }
        System.out.println("=================修改房屋成功==================");
    }

    //根据id查找房屋信息
    //编写findHouse()接收输入的id，调用Service的find方法
    public void findHouse() {
        System.out.println("=================查找房屋==================");
        System.out.print("请输入待查找房屋id(-1退出查找)");
        int findId = Utility.readInt();
        if (findId == -1) {
            System.out.println("=================已退出删除房屋==================");
            return;
        }

        //执行查找
        if (houseService.findById(findId) != null) {
            House house = houseService.findById(findId);
            System.out.println(house);
            System.out.println("=================查找房屋成功==================");
        } else {
            System.out.println("=================查找房屋失败==================");
        }
    }

    //退出
    public void exit() {
        char c = Utility.readConfirmSelection();
        if (c == 'Y') {
            loop = false;
        }
    }

    //删除房屋信息
    //编写delHouse()接收输入的id，调用Service的 del方法
    public void delHouse() {
        System.out.println("=================删除房屋==================");
        System.out.print("请输入待删除房屋id(-1退出删除)");
        int delId = Utility.readInt();
        if (delId == -1) {
            System.out.println("=================已退出删除房屋==================");
            return;
        }
        //该方法本身有循环，必须输出Y/N
        char choice = Utility.readConfirmSelection();
        if (choice == 'Y') {
            //执行删除
            if (houseService.del(delId)) {
                System.out.println("=================删除房屋成功==================");
            } else {
                System.out.println("=================删除房屋失败==================");
            }

        } else {
            System.out.println("=================退出删除房屋==================");
        }
    }

    //添加房屋
    //编写addhouse()接收数据，创建House对象，调用add()方法
    public void addHouse() {
        System.out.println("=================添加房屋==================");
        System.out.println("姓名：");
        String name = Utility.readString(8);
        System.out.println("电话：");
        String phone = Utility.readString(12);
        System.out.println("地址：");
        String address = Utility.readString(16);
        System.out.println("月租：");
        int rent = Utility.readInt();
        System.out.println("状态：");
        String state = Utility.readString(3);
        //创建一个新的House对象，注意id是系统分配，用户不能添加
        House newHouse = new House(0, name, phone, address, rent, state);
        if (houseService.add(newHouse)) {
            System.out.println("=================添加房屋成功==================");
        } else {
            System.out.println("=================添加房屋失败==================");
        }
    }

    //显示房屋列表
    public void listHouses() {
        System.out.println("=================房屋列表==================");
        System.out.println("编号\t\t房主\t\t电话\t\t地址\t\t月租\t\t状态（未出租/已出租）");
        House[] houses = houseService.list(); //获取到所有房屋信息
        for (int i = 0; i < houses.length; i++) {
            if (houses[i] == null) {
                break;
            }
            System.out.println(houses[i]);
        }
        System.out.println("=============房屋列表显示完毕==============\n");
    }

    //显示主菜单
    public void mainMenu() {
        do {
            System.out.println("=============房屋租赁系统菜单==============");
            System.out.println("\t\t\t1 新 增 房 源");
            System.out.println("\t\t\t2 查 找 房 源");
            System.out.println("\t\t\t3 删 除 房 源 信 息");
            System.out.println("\t\t\t4 修 改 房 源 信 息");
            System.out.println("\t\t\t5 房 屋 列 表");
            System.out.println("\t\t\t6 退       出");
            System.out.println("请输入你的选择（1-6）");
            key = Utility.readChar();
            switch (key) {
                case '1':
                    //System.out.println("新增");
                    addHouse();
                    break;
                case '2':
                    //System.out.println("查找 ");
                    findHouse();
                    break;
                case '3':
                    //System.out.println("删除");
                    delHouse();
                    break;
                case '4':
                    //System.out.println("修改");
                    updateHouse();
                    break;
                case '5':
                    //System.out.println("房屋列表");
                    listHouses();
                    break;
                case '6':
                    //System.out.println("退出");
                    exit();
                    break;
            }
        } while (loop);
    }
}
```

#### 3-3-3 HouseService类

HouseService类用于给HouseView类传输相应的数据，如HouseView中有listHouse()方法，而HouseService中的list()方法用于给listHouse()方法传送房屋列表的信息。

```java
package com.coderq.houserent.service;

import com.coderq.houserent.domain.House;

/**
 * Created by Q on 2022/2/26.
 *
 * 业务层
 * 定义House[],保存House对象
 * 1.响应HouseView的调用
 * 2.完成对房屋信息的增删改查（crud）
 */
public class HouseService {
    private House[] houses; //保存House对象
    private int houseNums = 1; //记录多少个房屋信息
    private int idCounter = 1; //记录当前Id增加到哪
    //构造器初始化数据
    public HouseService(int size) {
        //new houses
        houses = new House[size]; //创建HouseService对象时，指定数组大小
        //伪造数据，配合测试
        houses[0] = new House(1,"coderq","188","安徽",500,"未出租");
    }

    //修改房屋信息


    //find方法,查找房屋信息,返回House对象或null
    public House findById(int findId){
        //先找到要查找的房屋对应的下标
        for (int i = 0; i < houseNums; i++) {
            if (findId == houses[i].getId() ){ //要查找的房屋（id）
                return houses[i];
            }
        }
        return null;
    }

    //del方法,删除房屋信息
    public boolean del(int delId){
        //先找到要删除的房屋对应的下标
        int index = -1;
        for (int i = 0; i < houseNums; i++) {
            if (delId == houses[i].getId() ){ //要删除的房屋（id），是数组下标为i的元素
                index = i;
            }
        }
        if (index == -1){
            //System.out.println("该房屋不存在");
            return false;
        }
        //如果找到,有点难度
        for (int i = index; i < houseNums - 1 ; i++) {
            houses[i] = houses[i+1];
        }
        houses[--houseNums] = null; //当前房屋信息最后一个 设置null
        return true;
    }

    //add方法，添加新对象，返回boolean
    public boolean add(House newHouse){
        //判断是否还可以添加，数组满如何扩容？
        if(houseNums == houses.length){
            System.out.println("数组已满，无法添加");
            return false;
        }
        //newHouse对象加入到数组
        houses[houseNums++] = newHouse;
        //id自增机制
        newHouse.setId(++idCounter);
        return true;
    }

    //list方法，返回houses
    public House[] list(){
        return houses;
    }
}
```

#### 3-3-4 HouseRentApp类

主程序启动类

```java
package com.coderq.houserent;

import com.coderq.houserent.view.HouseView;

/**
 * Created by Q on 2022/2/26.
 */
public class HouseRentApp {
    public static void main(String[] args) {
        //创建HouseView对象，显示主菜单，程序入口
        new HouseView().mainMenu();
        System.out.println("=============你退出了系统==============");

    }
}

```

## 结束语

以上就是房屋出租系统的全部内容, 本项目也算是Java基础的一个小案例, 增删两个功能看着老韩的视频逐步写下来的，查改是自己尝试了去实现一下，然后发现自己实现确实思路上还有点乱，磕磕绊绊也算是最终实现了。本项目也算简单有了一点增删改查的小锻炼，希望接下来的岁月里继续脚踏实地，努力努力再努力。