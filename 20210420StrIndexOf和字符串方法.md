```
输入：haystack = "hello", needle = "ll"
输出：2
```

```java
class Solution {
    public int strStr(String haystack, String needle) {
        int num = haystack.indexOf(needle);
        return num;

    }
}
```

考察了java的基础知识，字符串方法

```java
String str ="abcdefg";

//获取字符串长度
str.length();
//获取字符串的指定字符
str.charAt();



public static void main(String[] args) {
		String str = "abcdefgdefghendiflalaallaa";
		
		str.charAt(0);
		System.out.println(str.charAt(0));
		
		//str.getChars(begin,end,array,arrayBegin);
		
		//Begin:开始位置
    	//end:结束位置
    	//array ；char型数组的名字
    	//开始储存的位置
		char str2[] = new char[20];
		str.getChars(0, 2,str2, 0);
		System.out.println(str2);     //ab
	}
```

### Java中char和String的区别

```java
char c='c';
//使用单引号

//只储存一个字符 

//char是基本数据类型

String str = "abc";
//使用双引号

//可以储存一个或者多个字符

//String是字符串，内部是char 字符数组；属于对象

```



