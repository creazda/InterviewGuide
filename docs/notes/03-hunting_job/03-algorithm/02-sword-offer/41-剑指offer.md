---
layout:  post
category:  algorithm
title:  No41、和为S的连续整数序列
tagline:  by 阿秀
tags:
    - 原创
    - 剑指offer
    - 数据结构与算法
    - 算法
    - 社招
    - 校招
    - 阿秀
excerpt: No41、和为S的连续整数序列
comment: false
---

<h1 align="center">带你快速刷完67道剑指offer</h1>

<div style="border-color: #24C6DC;
            background-color: #e9f9f3;         
            margin: 1rem 0;
        padding: .25rem 1rem;
        border-left-width: .3rem;
        border-left-style: solid;
        border-radius: .5rem;
        color: inherit;">
  <p>这是四则或许对你有些许帮助的信息:</p>
  <p>1、👉 最近我发现了一个每日都会推送最新校招资讯的《校招日程》文档，其中包括<a style="text-decoration: underline" href="https://flowus.cn/share/ee50d5eb-3cd5-4f74-880e-95b215dd4ff2" target="_blank">往届补录</a>、<a style="text-decoration: underline" href="https://flowus.cn/share/5f327c98-1e31-46c8-b86b-5ac6105e021f" target="_blank">应届实习校招</a>信息，比如各种大厂、国企、银行、事业编等信息都会定期更新，帮忙扩散一下。</p>  
  <p>2、😍
    免费分享阿秀个人学习计算机以来收集到的免费学习资源，<a style="text-decoration: underline" href="/notes/07-resources/01-free/01-introduce.html" target="_blank">点此白嫖</a>；也记录一下自己以前买过的<a style="text-decoration: underline" href="/notes/07-resources/02-precious.html" target="_blank">不错的计算机书籍、网络专栏和垃圾付费专栏</a>。
  </p>
  <p>3、🚀如果你想在校招中顺利拿到更好的offer，阿秀建议你多看看前人<a style="text-decoration: underline" href="https://www.yuque.com/tuobaaxiu/httmmc/npg1k81zeq4wfpyz" target="_blank">踩过的坑</a>和<a style="text-decoration: underline"  target="_blank" href="https://www.yuque.com/tuobaaxiu/httmmc/gge9ppd0mbu2d3dp">留下的经验</a>，事实上你现在遇到的大多数问题你的学长学姐师兄师姐基本都已经遇到过了。
  </p>
  <p>4、🔥 欢迎准备计算机校招的小伙伴加入我的<a  style="text-decoration: underline" href="https://www.yuque.com/tuobaaxiu/httmmc/xg0otqvc17wfx4u9" target="_blank">学习圈子</a>，一个人踽踽独行不如一群人报团取暖，圈子里沉淀了很多过去21/22/23届学长学姐的<a  style="text-decoration: underline" href="https://www.yuque.com/tuobaaxiu/httmmc/gge9ppd0mbu2d3dp" target="_blank">经验和总结</a>，好好跟着走下去的，最后基本都可以拿到不错的offer！此外，每周都会进行<a  style="text-decoration: underline" href="https://www.yuque.com/tuobaaxiu/httmmc/npg1k81zeq4wfpyz" target="_blank">精华总结和分享！</a>如果你需要《阿秀的学习笔记》网站中📚︎校招八股文相关知识点的PDF版本的话，可以<a style="text-decoration: underline" href="https://www.yuque.com/tuobaaxiu/httmmc/qs0yn66apvkzw0ps" target="_blank">点此下载</a> 。</p>   </div>



## **No41、和为S的连续整数序列**

<font style="font-weight:normal; color:#4169E1;text-decoration:underline;" target="_blank">[牛客网原题链接](https://www.nowcoder.com/practice/c451a3fd84b64cb19485dad758a55ebe?tpId=13&&tqId=11194&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)</font>

### **题目描述**

 小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck! 

**输出描述:**

```
输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序
```

输入
~~~
9
~~~
**返回值**

~~~
[[2,3,4],[4,5]]
~~~



### **1、牛客解法，很厉害，类似于TCP滑动窗口**

~~~cpp
vector<vector<int> > FindContinuousSequence(int sum) {
    vector<vector<int>> result;
    int low=1,high=2;//两个起点，相当于动态窗口的两边，根据其窗口内的值的和来确定窗口的位置和大小
    while(low<high){
        int sumTemp = (low+high) *(high-low +1)/2;
        //由于是连续的，差为1的一个序列，那么求和公式是(a0+an)*n/2
        if(sumTemp == sum){  //相等，那么就将窗口范围的所有数添加进结果集
            vector<int> resultTemp;
            for(int i=low;i<=high;++i)
            {resultTemp.push_back(i);}
            result.push_back(resultTemp);
            low++;
        }else if(sumTemp<sum){ //如果当前窗口内的值之和小于sum，那么右边窗口右移一下
            high++;
        }
        else{  //如果当前窗口内的值之和大于sum，那么左边窗口右移一下
            low++;
        }
    }
    return result;
}
~~~



### **2、暴力解法**

~~~cpp
vector<vector<int> > FindContinuousSequence(int sum) {
    vector<vector<int> > result;
    for (int n = sqrt(2 * sum); n >= 2; --n) {
        if (((n & 1) == 1 && sum % n == 0) || (sum % n * 2 == n)) {
            vector<int> res;
            //j用于计数，k用于遍历求值
            for (int j = 0, k = sum / n - (n - 1) / 2; j < n; j++, k++)//注意看k的求法
                res.push_back(k);
            result.push_back(res);
        }
    }
    return result;
}
~~~



### **二刷：**

### **1、滑动窗口，直接用数学公式来进行计算**

运行时间：3ms  占用内存：496k

~~~cpp
vector<vector<int> > FindContinuousSequence(int sum) {
    vector<vector<int>> result;
    int low = 1,high = 2;
    while(low < high){
        int sumTemp = (low + high) * (high - low + 1)/2;
        if(sumTemp == sum){
            vector<int> temp;
            for(int i = low;i <= high; ++i)
                temp.push_back(i);
            result.push_back(std::move(temp));
            low++;//即使当前满足，那么依然要前进的，这有点滑动窗口的意思吧
        }else if(sumTemp < sum) high++;
        else
            low++;
    }
    return std::move(result);//借助C++11的move函数，总体时间会更短    
}
~~~



### <font style="font-weight:normal; color:#4169E1;text-decoration:underline;" target="_blank">[力扣网原题链接](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)</font>

执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户

内存消耗：6.9 MB, 在所有 C++ 提交中击败了39.52%的用户

~~~cpp
vector<vector<int>> findContinuousSequence(int target) {

    vector<vector<int>> result;
    int low = 1,high = 2;
    while(low < high){
        int sumTemp = (low + high) * (high - low + 1)/2;
        if(sumTemp == target){
            vector<int> temp;
            for(int i = low;i <= high; ++i)
                temp.push_back(i);
            result.push_back(std::move(temp));
            low++;
        }else if(sumTemp < target) high++;
        else
            low++;
    }
    return std::move(result);//借助C++11的move函数，总体时间会更短    
}
~~~


<p id = "和为S的连续整数序列"></p>

