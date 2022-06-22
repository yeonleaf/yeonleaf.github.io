---
title: "(48) Rotate Image"
excerpt: ""

categories:
    - algorithm
tags:
    - [leetcode, medium, practice finished, ⭐]

toc: true

date: 2022-06-21
last_modified_at: 2022-06-22
---

## **문제 링크**
[Question Link](https://leetcode.com/problems/rotate-image/)

<br>

---
---
 
## **CODE 1**: 시간 초과
### <u>날짜</u> 2022-06-21
#### <u>총 소요시간</u> 

<br>

#### <u>다른 방식</u>
[Discusstion Link](https://leetcode.com/problems/rotate-image/discuss/18872/A-common-method-to-rotate-the-image)

이거 외우기!!!

```cpp
/*
 * clockwise rotate
 * first reverse up to down, then swap the symmetry 
 * 1 2 3     7 8 9     7 4 1
 * 4 5 6  => 4 5 6  => 8 5 2
 * 7 8 9     1 2 3     9 6 3
*/
void rotate(vector<vector<int> > &matrix) {
    reverse(matrix.begin(), matrix.end());
    for (int i = 0; i < matrix.size(); ++i) {
        for (int j = i + 1; j < matrix[i].size(); ++j)
            swap(matrix[i][j], matrix[j][i]);
    }
}

/*
 * anticlockwise rotate
 * first reverse left to right, then swap the symmetry
 * 1 2 3     3 2 1     3 6 9
 * 4 5 6  => 6 5 4  => 2 5 8
 * 7 8 9     9 8 7     1 4 7
*/
void anti_rotate(vector<vector<int> > &matrix) {
    for (auto vi : matrix) reverse(vi.begin(), vi.end());
    for (int i = 0; i < matrix.size(); ++i) {
        for (int j = i + 1; j < matrix[i].size(); ++j)
            swap(matrix[i][j], matrix[j][i]);
    }
}
```

---
---

<br>

---
---
 
## **CODE 2**: ACCEPTED
### <u>날짜</u> 2022-06-22
#### <u>총 소요시간</u> 20m

<br>

#### <u>설계</u>
```python
'''
위와 아래를 바꾼다.
대칭되는 값을 swap한다.

15 14 12 16
13 3 6 7
2 4 8 10
5 1 9 11
n = len(matrix)
1부터 n//2까지
i와 n-i-1을 교체

대칭되는 값을 swap
'''
```

<br>

#### <u>코드</u>
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        
        n = len(matrix)
        for i in range(n//2):
            matrix[i], matrix[n-i-1] = matrix[n-i-1], matrix[i]
        
        for row in matrix:
            print(*row)
        
        for i in range(n):
            for j in range(i, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
                
```

```python
for i in range(n):
    for j in range(i, n):
```
for문의 범위 주의! (n, n으로 지정하면 i, j일 때 한 번 swap하고 j, i일때 한 번 더 swap해서 결국 원래대로 돌아오게 된다.)



---
---
