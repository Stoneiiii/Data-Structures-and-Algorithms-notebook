# Closest Points

## Problem Introduction

    In this problem, your goal is to find the closest pair of points among the given 𝑛 points. This is a basic primitive in computational geometry having applications in, for example, graphics, computer vision, traffic-control systems.
![week4_divide_and_conquer.jpg](attachment:891a5cca-744f-4f0d-9c9f-4865b484a333.jpg)

## Problem Description

### Task.

Given 𝑛 points on a plane, find the smallest distance between a pair of two (different) points. Recall that the distance between points (𝑥1, 𝑦1) and (𝑥2,𝑦2) is equal to  $\sqrt{(𝑥1 − 𝑥2)^2 + (𝑦1 − 𝑦2)^2}$

## Input Format

The first line contains the number 𝑛 of points. Each of the following 𝑛 lines defines a point (𝑥𝑖, 𝑦𝑖).

## Constraints

$2 ≤ 𝑛 ≤ 10^5; −10^9 ≤ 𝑥𝑖, 𝑦𝑖 ≤ 10^9 $are integers.

## Output Format.

Output the minimum distance. The absolute value of the difference between the answer of your program and the optimal value should be at most $10^{−3}$. To ensure this, output your answer with at least four digits after the decimal point (otherwise your answer, while being computed correctly, can turn out to be wrong because of rounding issues).

## Sample 1

Input:  
2  
0 0  
3 4  
Output:  
5.0  
There are only two points here. The distance between them is 5.

## Sample 2

Input:  
4  
7 7  
1 100  
4 8  
7 7  
Output:  
0.0  
There are two coinciding points among the four given points. Thus, the minimum distance is zero.

## Sample 3

Input:  
11  
4 4  
-2 -2  
-3 -4  
-1 3  
2 3  
-4 0  
1 1  
-1 -1  
3 -1  
-4 2  
-2 4  
Output:  
1.414213  
The smallest distance is $\sqrt{2}$. There are two pairs of points at this distance: (−1,−1) and (−2,−2); (−2, 4) and (−1, 3).

--------

# 思路

分治思路，二分法递归查找2边最小长度d，然后查找二分的分割线 ±d 距离内一左一右是否有比d小的2点长度的点。  
问题在于，如果暴力搜索分割线附近，还是O($n^2$)了。![image.png](attachment:0c09311d-1601-42fb-8f2c-8b4cf4c41c37.png)

精妙在于:符合鸽巢定理。最多对于任意左边符合条件的点，在右边区域最多存在6个。
下面证明

以L为中心，δ为半径划分一个区域，最小点对还有可能存在于SL和SR的交界处，例如p点和q点分别位于SL和SR的虚线范围内。只有在这个范围内，p点和q点之间的距离才会小于δ

因为前面二分法对于SR和SL区域已经查找出了最小距离为δ，所以SR和SL区域中任何2点的距离都不小于δ（但可能存在一个在SL一个在SR，距离还小于δ，所以这里要查找比较）。不选取2δ带中所有的点进行计算，而是对于SL虚框范围内的任一p点，只选取SR虚框范围内长2δ，宽为δ的中的点进行计算（如下图）。由此可以推出矩形R中最多只有6个SR中的点（红点）。推理如下  
![image.png](attachment:34b54e4e-da30-4378-9a25-f2042be0b189.png)

## 证明

2. 反证法  
    如果右边这2个正方形内有7个点（2个四边形的6个端点和点q）与p点距离小于δ，例如q点，则q点与下面正方形的四个顶点距离小于δ，则和δ为SL和SR中的最小点对距离相矛盾。因此对于SL虚框中的p点，最多存在6个点与p距离小于δ
    ![image.png](attachment:c13c5c5b-1edd-4128-8fef-44153c26730b.png)

2. 鸽舍原理  
由δ的意义可知区域中任何2个点的距离都不小于δ。由此可以推出矩形R中最多只有6的点。事实上，我们可以将矩形R的长为2δ的边3等分，将它的长为δ的边2等分，由此导出6个（δ/2）×（2δ/3）的矩形（虚线分割）。
![image.png](attachment:4fb3d07f-d74d-44df-a321-bc9f0e2a722a.png)
若矩形R中有多于6个点，则由鸽舍原理可知至少有一个虚线分割的的小矩形中有2个以上的点。设u,v是这样2个点，它们位于同一小矩形中，则因此u和v 2点的距离d≤$\frac{5}{6}$δ<δ 。这与δ的意义(区域中任何2个点的距离都不小于δ)相矛盾

----

## 代码如下


```python
#Uses python3
import sys
import math

def length(point1, point2): #计算2点距离
    return math.sqrt(pow(point2[1]-point1[1],2) + pow(point2[0]-point1[0],2))

def minimum_distance(a, start, end):
    #write your code here
    if len(a) == 1: #只有1个点，没有距离
        return 0
    elif len(a) == 2: #只有2个点
        return length(a[0],a[1])
    d = 0
    if (end- start) < 1: #二分结束一个点的情况，不能返回0，要返回一个任意2点距离都比之小的值，即无穷大。
        return float("inf")
    if (end- start) == 1:#二分结束还剩2个点的情况
        return length(a[start],a[end])

    mid = start + (end - start) //2
    l = minimum_distance(a, start, mid)
    r = minimum_distance(a, mid + 1, end)
    
    if l > r:
        d = r
    else:
        d = l

    lmin = d  #lmin 记录一点在分割线左，一点在右产生的小于d最小值
    points = [] #把在分割线±d区域的点找出来，不用分左右，因为已经二分查找了，同一边的点距离肯定大于d
    for i in range(start, end+1):
        if abs(a[i][0] - a[mid][0]) <= d:
            points.append(a[i])
    points = sorted(points, key=lambda x: x[1])  #按y轴坐标排序，方便向后查找6个点。（可不用）

    if len(points) < 2:
        return d
    else:
        for i in range(len(points)-1):
            for j in range(i+1, min(i + 7, len(points))): #至多只用在看6个点
                    if length(points[i],points[j]) <= d:
                        if lmin > length(points[i],points[j]):
                            lmin = length(points[i],points[j])
    return lmin

if __name__ == '__main__':
    input = sys.stdin.read()
    data = list(map(int, input.split()))
    n = data[0]
    x = data[1::2]
    y = data[2::2]
    a = sorted(zip(x,y), key=lambda x: (x[0], x[1]))
    print("{0:.9f}".format(minimum_distance(a, 0, len(a)-1)))
```
