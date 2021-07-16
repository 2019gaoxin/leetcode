#### [1418. 点菜展示表](https://leetcode-cn.com/problems/display-table-of-food-orders-in-a-restaurant/)

```java
输入：orders = [["David","3","Ceviche"],["Corina","10","Beef Burrito"],["David","3","Fried Chicken"],["Carla","5","Water"],["Carla","5","Ceviche"],["Rous","3","Ceviche"]]
输出：[["Table","Beef Burrito","Ceviche","Fried Chicken","Water"],["3","0","2","1","0"],["5","0","1","0","1"],["10","1","0","0","0"]] 
解释：
点菜展示表如下所示：
Table,Beef Burrito,Ceviche,Fried Chicken,Water
3    ,0           ,2      ,1            ,0
5    ,0           ,1      ,0            ,1
10   ,1           ,0      ,0            ,0
对于餐桌 3：David 点了 "Ceviche" 和 "Fried Chicken"，而 Rous 点了 "Ceviche"
而餐桌 5：Carla 点了 "Water" 和 "Ceviche"
餐桌 10：Corina 点了 "Beef Burrito" 

来源：力扣（LeetCode）
```

List、Set和Map的灵活使用


```java
package com.leetcode.demo;

import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class ListDouble {
	public static List<List<String>> orders1 = new ArrayList<List<String>>();
	
	public static List<List<String>> displayTable(List<List<String>> orders) {
		Map<Integer,Map<String,Integer>> foodMap = new HashMap<Integer,Map<String,Integer>>();
        
        List<List<String>> end = new ArrayList<List<String>>();
        //使用Set统计菜的名称
        Set<String> namesSet = new HashSet<>();
        //现在可以把TableNum打印出来
        
        //***************用一组循环来把oders中的数据进行统计。
        
        for(List<String> list:orders){
           String num = list.get(1);
           String name = list.get(2);
           //同时完成对名字的统计
           int id = Integer.parseInt(num);//这个BUG我找看两个小时，因为NUM为String类型
           namesSet.add(name);

           Map<String,Integer> map = foodMap.get(id);//这个BUG     一定不要传num（String）
           //map.put(list.get(2), map.getOrDefault(list.get(2), 0) + 1);
           if(map == null) {
        	   map = new HashMap<String,Integer>();
        	   System.out.println("NUll");
           }
           //Map<String, Integer> map = foodMap.getOrDefault(num, new HashMap<String, Integer>());


           Integer n = map.get(name);
           if(n==null) {
        	   //map.put(name, 1);
        	   n = 1;
        	   //System.out.println("Null");
           }else {     
        	   System.out.println("执行");
        	   //map.put(name, n+1);
        	   n++;
        	   
           }
           //把小map加入到大Map里面
           System.out.println(name + n);
           map.put(name, n);
           System.out.println(num);
          
           foodMap.put(id, map);
           
           //System.out.println("放入成功");

           //System.out.println(num);
        }
        
        
        //********************第二模块:完成表头
        
        //结果中第一个list是菜名，所以先创建菜名list
        List<String> namelist = new ArrayList<String>();
        for(String name:namesSet) {
        	namelist.add(name);
        }
        //end.add(namelist); 注意还有一个Table
        
        //首先进行排序按菜名的首字母
        Collections.sort(namelist);
        //再把Table加进来
        List<String> firstList = new ArrayList<>();
        
        firstList.add("Table");
        
        for(String str: namelist) {
        	
        	firstList.add(str);
        	
        }
        
        end.add(firstList);
        
        
        //********************第三个模块统计桌号
        
        //题目要求从小到大 升序。
        List<Integer> tableList =new ArrayList<Integer>();
        for(int n:foodMap.keySet()) {
        	tableList.add(n);
        }
        Collections.sort(tableList);
        //*******************第四个模块 把数据装入end
        
        for(int i = 0 ;i<tableList.size();i++) {
        	
        	Map<String,Integer> map = foodMap.get(tableList.get(i));
        	
        	List<String> row = new ArrayList<>();
        	row.add(Integer.toString(tableList.get(i)));
        	for(int j = 0;j< namesSet.size();j++) {
        		row.add(Integer.toString(map.getOrDefault(namelist.get(j), 0)));
        		
        	}
        	
        	end.add(row);
        	
        }
        
        

        return end;
    }
	
	public static void main(String[] args) {
		inintOrders();
		
		
		displayTable(orders1);
	}
	
	public static void inintOrders() {
		List<String> l1 = new ArrayList<>();
		l1.add("David");
		l1.add("3");
		l1.add("Ceviche");
		orders1.add(l1);
		
		List<String> l2 = new ArrayList<>();
		l2.add("Corina");
		l2.add("10");
		l2.add("Beef Burrito");
		orders1.add(l2);
		
		List<String> l3 = new ArrayList<>();
		l3.add("David");
		l3.add("3");
		l3.add("Fried Chicken");
		orders1.add(l3);
		
		List<String> l4 = new ArrayList<>();
		l4.add("Carla");
		l4.add("5");
		l4.add("Water");
		orders1.add(l4);
		
		
		
		List<String> l5 = new ArrayList<>();
		l5.add("Carla");
		l5.add("5");
		l5.add("Ceviche");
		orders1.add(l5);
		
		List<String> l6 = new ArrayList<>();
		l6.add("Rous");
		l6.add("3");
		l6.add("Ceviche");
		orders1.add(l6);
	}

}

```

