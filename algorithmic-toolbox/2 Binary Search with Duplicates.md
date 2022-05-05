# Binary Search with Duplicates

## Problem Description

## Task

    Find the first occurence of an integer in the given sorted sequence of integers (possibly with duplicates).

## Input Format

    The first two lines of the input contain an integer 𝑛 and a sequence 𝑎0 ≤ 𝑎1 ≤ · · · ≤ 𝑎𝑛−1 of 𝑛 positive integers in non-decreasing order. The next two lines contain an integer 𝑘 and 𝑘 positive integers 𝑏0, 𝑏1, . . . , 𝑏𝑘−1.

## Constraints

    1 ≤ 𝑘 ≤ 10^5; 1 ≤ 𝑛 ≤ 3 · 10^4; 1 ≤ 𝑎𝑖 ≤ 10^9 for all 0 ≤ 𝑖 < 𝑛; 1 ≤ 𝑏𝑗 ≤ 10^9 for all 0 ≤ 𝑗 < 𝑘;

## Output Format

    For all 𝑖 from 0 to 𝑘−1, output an index 0 ≤ 𝑗 ≤ 𝑛−1 of the first occurrence of 𝑏𝑖 (i.e., 𝑎𝑗 = 𝑏𝑖) or −1 if there is no such index.

## Sample 1

Input:  
7  
2 4 4 4 7 7 9  
4  
9 4 5 2  
Output:  
6 1 -1 0

---

## 思路

带有重复值，要返回重复值的第一个目标元素的位置。
首先的想法是：在基础的二分法上进行回溯，向前查找N次是否为相同元素，返回边界即可。


```python
# r:right 字符串右边界
# l:left 字符串左边界
# keys 非逆序数组
# query 目标元素
def binary_search(keys, query,l,r):
    if l > r:
        return -1
    m = int((l+r)/2)
    if keys[m] == query:
        while m>=0:    #找到了后向上遍历，寻找相等元素边界
            if keys[m] != query:
                break
            m = m - 1
        if m <= -1:
            return 0
        return m + 1
    elif keys[m] < query:
        t = keys[m]
        while m<=r:     #错误观念：想着有大面积相同元素，向下遍历找到边界，节约时间
            if keys[m] != t:
                break
            m = m + 1
        if m >= r+1:
            m = r+1
        else:
            m = m 
        l = m 
        return binary_search(keys, query,l,r)
    else:
        t = keys[m]
        while m>=0:   #错误观念：想着有大面积相同元素，向上遍历找到边界，节约时间
            if keys[m] != t:
                break
            m = m -1
        if m <= -1:
            m = -1
        else:    
            m = m
        r = m
        return binary_search(keys, query,l,r)
 

if __name__ == '__main__':
    num_keys = int(input())
    input_keys = list(map(int, input().split()))
    assert len(input_keys) == num_keys

    num_queries = int(input())
    input_queries = list(map(int, input().split()))
    assert len(input_queries) == num_queries

    r = len(input_keys)-1
    l = 0
    for q in input_queries:
        print(binary_search(input_keys, q,l,r), end=' ')
    

```

     7
     2 4 4 4 7 7 9
     4
     4 9 2 1
    

    1 6 0 -1 

上面程序能正常得出结果，但TLE了。  
分析得知:自己傻逼了    
二分法时间复杂度:O(log(n))  
加上回溯寻找边界的时间复杂度O(n)  (最坏情况下要一次二分后，遍历数组长度的一半)  
结果代码总时间复杂度：O(n)了。。  
**所以不需要遍历，找到相等元素后，记录元素位置，继续二分法，直到二分结束为止**  
**时间复杂度依旧：O(log(n))**


```python
def binary_search2(keys, n, element):
    l0 = 0
    hi = n
    output = -1
    while hi > l0:
        mid = l0 + (hi-l0) // 2
        val = keys[mid]
        if (val < element):
            l0 = mid + 1
        elif (val > element):
            hi = mid
        else:
            output = mid
            hi = mid
    return output

if __name__ == '__main__':
    num_keys = int(input())
    input_keys = list(map(int, input().split()))
    assert len(input_keys) == num_keys

    num_queries = int(input())
    input_queries = list(map(int, input().split()))
    assert len(input_queries) == num_queries

    r = len(input_keys)-1
    l = 0
    for q in input_queries:
        #print(binary_search(input_keys, q,l,r), end=' ')
        print(binary_search2(input_keys, r+1,q), end=' ')
```

     7
     2 4 4 4 7 7 9
     4
     4 9 2 1
    

    1 6 0 -1 
