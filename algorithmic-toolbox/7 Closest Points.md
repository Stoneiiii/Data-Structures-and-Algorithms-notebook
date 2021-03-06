# Closest Points

## Problem Introduction

    In this problem, your goal is to find the closest pair of points among the given ๐ points. This is a basic primitive in computational geometry having applications in, for example, graphics, computer vision, traffic-control systems.
![ไธ่ฝฝ](https://user-images.githubusercontent.com/41032510/167538241-edf1d543-89f8-4e7f-b1f5-6a1d5fc5d589.jpg)


## Problem Description

### Task.

Given ๐ points on a plane, find the smallest distance between a pair of two (different) points. Recall that the distance between points (๐ฅ1, ๐ฆ1) and (๐ฅ2,๐ฆ2) is equal to  $\sqrt{(๐ฅ1 โ ๐ฅ2)^2 + (๐ฆ1 โ ๐ฆ2)^2}$

## Input Format

The first line contains the number ๐ of points. Each of the following ๐ lines defines a point (๐ฅ๐, ๐ฆ๐).

## Constraints

$2 โค ๐ โค 10^5; โ10^9 โค ๐ฅ๐, ๐ฆ๐ โค 10^9 $are integers.

## Output Format.

Output the minimum distance. The absolute value of the difference between the answer of your program and the optimal value should be at most $10^{โ3}$. To ensure this, output your answer with at least four digits after the decimal point (otherwise your answer, while being computed correctly, can turn out to be wrong because of rounding issues).

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
The smallest distance is $\sqrt{2}$. There are two pairs of points at this distance: (โ1,โ1) and (โ2,โ2); (โ2, 4) and (โ1, 3).

--------

# ๆ่ทฏ

ๅๆฒปๆ่ทฏ๏ผไบๅๆณ้ๅฝๆฅๆพ2่พนๆๅฐ้ฟๅบฆd๏ผ็ถๅๆฅๆพไบๅ็ๅๅฒ็บฟ ยฑd ่ท็ฆปๅไธๅทฆไธๅณๆฏๅฆๆๆฏdๅฐ็2็น้ฟๅบฆ็็นใ  
้ฎ้ขๅจไบ๏ผๅฆๆๆดๅๆ็ดขๅๅฒ็บฟ้่ฟ๏ผ่ฟๆฏO($n^2$)ไบใ![ไธ่ฝฝ](https://user-images.githubusercontent.com/41032510/167538454-ef56b0e2-51bf-46e9-9151-1f0ebbd03d1d.png)

็ฒพๅฆๅจไบ:็ฌฆๅ้ธฝๅทขๅฎ็ใๆๅคๅฏนไบไปปๆๅทฆ่พน็ฌฆๅๆกไปถ็็น๏ผๅจๅณ่พนๅบๅๆๅคๅญๅจ6ไธชใ
ไธ้ข่ฏๆ

ไปฅLไธบไธญๅฟ๏ผฮดไธบๅๅพๅๅไธไธชๅบๅ๏ผๆๅฐ็นๅฏน่ฟๆๅฏ่ฝๅญๅจไบSLๅSR็ไบค็ๅค๏ผไพๅฆp็นๅq็นๅๅซไฝไบSLๅSR็่็บฟ่ๅดๅใๅชๆๅจ่ฟไธช่ๅดๅ๏ผp็นๅq็นไน้ด็่ท็ฆปๆไผๅฐไบฮด

ๅ?ไธบๅ้ขไบๅๆณๅฏนไบSRๅSLๅบๅๅทฒ็ปๆฅๆพๅบไบๆๅฐ่ท็ฆปไธบฮด๏ผๆไปฅSRๅSLๅบๅไธญไปปไฝ2็น็่ท็ฆป้ฝไธๅฐไบฮด๏ผไฝๅฏ่ฝๅญๅจไธไธชๅจSLไธไธชๅจSR๏ผ่ท็ฆป่ฟๅฐไบฮด๏ผๆไปฅ่ฟ้่ฆๆฅๆพๆฏ่พ๏ผใไธ้ๅ2ฮดๅธฆไธญๆๆ็็น่ฟ่ก่ฎก็ฎ๏ผ่ๆฏๅฏนไบSL่ๆก่ๅดๅ็ไปปไธp็น๏ผๅช้ๅSR่ๆก่ๅดๅ้ฟ2ฮด๏ผๅฎฝไธบฮด็ไธญ็็น่ฟ่ก่ฎก็ฎ๏ผๅฆไธๅพ๏ผใ็ฑๆญคๅฏไปฅๆจๅบ็ฉๅฝขRไธญๆๅคๅชๆ6ไธชSRไธญ็็น๏ผ็บข็น๏ผใๆจ็ๅฆไธ  
![ไธ่ฝฝ (1)](https://user-images.githubusercontent.com/41032510/167538515-8f04879d-2a66-46cc-8e80-11002f3419e9.png)

## ่ฏๆ

2. ๅ่ฏๆณ  
    ๅฆๆๅณ่พน่ฟ2ไธชๆญฃๆนๅฝขๅๆ7ไธช็น๏ผ2ไธชๅ่พนๅฝข็6ไธช็ซฏ็นๅ็นq๏ผไธp็น่ท็ฆปๅฐไบฮด๏ผไพๅฆq็น๏ผๅq็นไธไธ้ขๆญฃๆนๅฝข็ๅไธช้กถ็น่ท็ฆปๅฐไบฮด๏ผๅๅฮดไธบSLๅSRไธญ็ๆๅฐ็นๅฏน่ท็ฆป็ธ็็พใๅ?ๆญคๅฏนไบSL่ๆกไธญ็p็น๏ผๆๅคๅญๅจ6ไธช็นไธp่ท็ฆปๅฐไบฮด
    ![ไธ่ฝฝ (2)](https://user-images.githubusercontent.com/41032510/167538564-0010f0c4-e13b-449c-a6d7-687939f5facd.png)

2. ้ธฝ่ๅ็  
็ฑฮด็ๆไนๅฏ็ฅๅบๅไธญไปปไฝ2ไธช็น็่ท็ฆป้ฝไธๅฐไบฮดใ็ฑๆญคๅฏไปฅๆจๅบ็ฉๅฝขRไธญๆๅคๅชๆ6็็นใไบๅฎไธ๏ผๆไปฌๅฏไปฅๅฐ็ฉๅฝขR็้ฟไธบ2ฮด็่พน3็ญๅ๏ผๅฐๅฎ็้ฟไธบฮด็่พน2็ญๅ๏ผ็ฑๆญคๅฏผๅบ6ไธช๏ผฮด/2๏ผร๏ผ2ฮด/3๏ผ็็ฉๅฝข๏ผ่็บฟๅๅฒ๏ผใ
![ไธ่ฝฝ (3)](https://user-images.githubusercontent.com/41032510/167538618-8352a99e-8d5f-4444-a883-82de526390bb.png)
่ฅ็ฉๅฝขRไธญๆๅคไบ6ไธช็น๏ผๅ็ฑ้ธฝ่ๅ็ๅฏ็ฅ่ณๅฐๆไธไธช่็บฟๅๅฒ็็ๅฐ็ฉๅฝขไธญๆ2ไธชไปฅไธ็็นใ่ฎพu,vๆฏ่ฟๆ?ท2ไธช็น๏ผๅฎไปฌไฝไบๅไธๅฐ็ฉๅฝขไธญ๏ผๅๅ?ๆญคuๅv 2็น็่ท็ฆปdโค$\frac{5}{6}$ฮด<ฮด ใ่ฟไธฮด็ๆไน(ๅบๅไธญไปปไฝ2ไธช็น็่ท็ฆป้ฝไธๅฐไบฮด)็ธ็็พ

----

## ไปฃ็?ๅฆไธ


```python
#Uses python3
import sys
import math

def length(point1, point2): #่ฎก็ฎ2็น่ท็ฆป
    return math.sqrt(pow(point2[1]-point1[1],2) + pow(point2[0]-point1[0],2))

def minimum_distance(a, start, end):
    #write your code here
    if len(a) == 1: #ๅชๆ1ไธช็น๏ผๆฒกๆ่ท็ฆป
        return 0
    elif len(a) == 2: #ๅชๆ2ไธช็น
        return length(a[0],a[1])
    d = 0
    if (end- start) < 1: #ไบๅ็ปๆไธไธช็น็ๆๅต๏ผไธ่ฝ่ฟๅ0๏ผ่ฆ่ฟๅไธไธชไปปๆ2็น่ท็ฆป้ฝๆฏไนๅฐ็ๅผ๏ผๅณๆ?็ฉทๅคงใ
        return float("inf")
    if (end- start) == 1:#ไบๅ็ปๆ่ฟๅฉ2ไธช็น็ๆๅต
        return length(a[start],a[end])

    mid = start + (end - start) //2
    l = minimum_distance(a, start, mid)
    r = minimum_distance(a, mid + 1, end)
    
    if l > r:
        d = r
    else:
        d = l

    lmin = d  #lmin ่ฎฐๅฝไธ็นๅจๅๅฒ็บฟๅทฆ๏ผไธ็นๅจๅณไบง็็ๅฐไบdๆๅฐๅผ
    points = [] #ๆๅจๅๅฒ็บฟยฑdๅบๅ็็นๆพๅบๆฅ๏ผไธ็จๅๅทฆๅณ๏ผๅ?ไธบๅทฒ็ปไบๅๆฅๆพไบ๏ผๅไธ่พน็็น่ท็ฆป่ฏๅฎๅคงไบd
    for i in range(start, end+1):
        if abs(a[i][0] - a[mid][0]) <= d:
            points.append(a[i])
    points = sorted(points, key=lambda x: x[1])  #ๆy่ฝดๅๆ?ๆๅบ๏ผๆนไพฟๅๅๆฅๆพ6ไธช็นใๅ?ไธบๆไธ้ขๅๆ๏ผๅ้ๅบๅๆฏไธไธช็ฉๅฝข๏ผไธyๅๆ?็้ด้ๅฐไบ็ญไบd๏ผๆไปฅๆๅฐๅผ่ฏๅฎๅบๅจy่ฝด้ด้่พ่ฟ็็น

    if len(points) < 2:
        return d
    else:
        for i in range(len(points)-1):
            for j in range(i+1, min(i + 7, len(points))): #่ณๅคๅช็จๅจ็6ไธช็น
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
