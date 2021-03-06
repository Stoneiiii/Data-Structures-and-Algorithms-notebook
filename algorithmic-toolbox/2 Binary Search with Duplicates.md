# Binary Search with Duplicates

## Problem Description

## Task

    Find the first occurence of an integer in the given sorted sequence of integers (possibly with duplicates).

## Input Format

    The first two lines of the input contain an integer ๐ and a sequence ๐0 โค ๐1 โค ยท ยท ยท โค ๐๐โ1 of ๐ positive integers in non-decreasing order. The next two lines contain an integer ๐ and ๐ positive integers ๐0, ๐1, . . . , ๐๐โ1.

## Constraints

    1 โค ๐ โค 10^5; 1 โค ๐ โค 3 ยท 10^4; 1 โค ๐๐ โค 10^9 for all 0 โค ๐ < ๐; 1 โค ๐๐ โค 10^9 for all 0 โค ๐ < ๐;

## Output Format

    For all ๐ from 0 to ๐โ1, output an index 0 โค ๐ โค ๐โ1 of the first occurrence of ๐๐ (i.e., ๐๐ = ๐๐) or โ1 if there is no such index.

## Sample 1

Input:  
7  
2 4 4 4 7 7 9  
4  
9 4 5 2  
Output:  
6 1 -1 0

---

## ๆ่ทฏ

ๅธฆๆ้ๅคๅผ๏ผ่ฆ่ฟๅ้ๅคๅผ็็ฌฌไธไธช็ฎๆ ๅ็ด ็ไฝ็ฝฎใ
้ฆๅ็ๆณๆณๆฏ๏ผๅจๅบ็ก็ไบๅๆณไธ่ฟ่กๅๆบฏ๏ผๅๅๆฅๆพNๆฌกๆฏๅฆไธบ็ธๅๅ็ด ๏ผ่ฟๅ่พน็ๅณๅฏใ


```python
# r:right ๅญ็ฌฆไธฒๅณ่พน็
# l:left ๅญ็ฌฆไธฒๅทฆ่พน็
# keys ้้ๅบๆฐ็ป
# query ็ฎๆ ๅ็ด 
def binary_search(keys, query,l,r):
    if l > r:
        return -1
    m = int((l+r)/2)
    if keys[m] == query:
        while m>=0:    #ๆพๅฐไบๅๅไธ้ๅ๏ผๅฏปๆพ็ธ็ญๅ็ด ่พน็
            if keys[m] != query:
                break
            m = m - 1
        if m <= -1:
            return 0
        return m + 1
    elif keys[m] < query:
        t = keys[m]
        while m<=r:     #้่ฏฏ่งๅฟต๏ผๆณ็ๆๅคง้ข็งฏ็ธๅๅ็ด ๏ผๅไธ้ๅๆพๅฐ่พน็๏ผ่็บฆๆถ้ด
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
        while m>=0:   #้่ฏฏ่งๅฟต๏ผๆณ็ๆๅคง้ข็งฏ็ธๅๅ็ด ๏ผๅไธ้ๅๆพๅฐ่พน็๏ผ่็บฆๆถ้ด
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

ไธ้ข็จๅบ่ฝๆญฃๅธธๅพๅบ็ปๆ๏ผไฝTLEไบใ  
ๅๆๅพ็ฅ:่ชๅทฑๅป้ผไบ    
ไบๅๆณๆถ้ดๅคๆๅบฆ:O(log(n))  
ๅ ไธๅๆบฏๅฏปๆพ่พน็็ๆถ้ดๅคๆๅบฆO(n)  (ๆๅๆๅตไธ่ฆไธๆฌกไบๅๅ๏ผ้ๅๆฐ็ป้ฟๅบฆ็ไธๅ)  
็ปๆไปฃ็ ๆปๆถ้ดๅคๆๅบฆ๏ผO(n)ไบใใ  
**ๆไปฅไธ้่ฆ้ๅ๏ผๆพๅฐ็ธ็ญๅ็ด ๅ๏ผ่ฎฐๅฝๅ็ด ไฝ็ฝฎ๏ผ็ปง็ปญไบๅๆณ๏ผ็ดๅฐไบๅ็ปๆไธบๆญข**  
**ๆถ้ดๅคๆๅบฆไพๆง๏ผO(log(n))**


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
