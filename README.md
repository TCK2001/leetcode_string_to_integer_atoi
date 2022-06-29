# leetcode_string_to_integer_atoi
+ String을 int로 전환후 숫자일경우 출력
+ 把string轉換成int之後再判斷是否數字來決定是否回傳

-----
+ Example1
```
Input: s = "42"
Output: 42
Explanation: The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-231, 231 - 1], the final result is 42.
```
----
+ Example2
```
Input: s = "   -42"
Output: -42
Explanation:
Step 1: "   -42" (leading whitespace is read and ignored)
            ^
Step 2: "   -42" ('-' is read, so the result should be negative)
             ^
Step 3: "   -42" ("42" is read in)
               ^
The parsed integer is -42.
Since -42 is in the range [-231, 231 - 1], the final result is -42.
```
----
+ Example3
```
Input: s = "4193 with words"
Output: 4193
Explanation:
Step 1: "4193 with words" (no characters read because there is no leading whitespace)
         ^
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "4193 with words" ("4193" is read in; reading stops because the next character is a non-digit)
             ^
The parsed integer is 4193.
Since 4193 is in the range [-231, 231 - 1], the final result is 4193.
```
----
```python
import re # regular expression사용하기 위한 라이브러리import
class Solution:
    def myAtoi(self, s: str) -> int:
        res = re.search(r"^ *([-+]?\d+)", s) # 시작이 공백(0개~무한개) 그리고 [-혹은+]가 있어도 되고 없어도 되고 숫자가 1하나 있을경우를 찾음
        if not res: # 만약 없으면 0을 반환
            return 0
        res = int(res.group(0)) # 모든 결과값 그룹화해서 하나의 문자열로 만들기
        return min(2**31-1, max(res, -2**31)) # < 2**31-1이거나 >-2**31일떄만 답을 리턴
```
---
```
결론 :
import해도 되는지 처음 알았다 이 문제는 도저히 해결이 안돼서 Rumotameru 코드를 보며 배웠다
```
---
```
結論:
第一次知道可以import XD 加上因為我寫的程式不知道他不行跑 所以到最後只好看 Rumotameru的程式碼去學習
```
---
### Result
Runtime: 43 ms, faster than 76.72% of Python3 online submissions for String to Integer (atoi).\
Memory Usage: 13.9 MB, less than 29.92% of Python3 online submissions for String to Integer (atoi).
### My first answer
```python
res = ''
check = ''
manager = 0
if s[0] == ' ' or s[0] == '+' or s[0] == '-' or ord(s[0]) >= 48 and ord(s[0]) <= 57: # 판단 첫번째가 공백,+,-,그리고 숫자일 경우
    if s[0] == ' ': # 만약 공백일경우 이어서 다음 코드
        pass
    elif s[1] == '+' or s[1] == '-': # 만약 다음것이 +이거나 -일경우 ex:+-11
        return(0) # 0을 반환
        manager = 1 # 밑에 판단식을 판단안함
    else: 첫번째만 + 혹은 - 일경우
        res += s[0] # res에 더 해줌
        s = s.replace(s[0],"") # 그리고 +와-지워서 밑에 판단식 돌입
        check = res + s # 최대크기 판단하기
    if s.isdigit() and int(check) < -2147483648: # 최대크기 넘을시 
        return(-2147483648) # 최대 답을 출력
    elif s.isdigit() and int(check) > 2147483648:
        return(2147483648) 
    elif manager == 0: # 만약 정상적인 input일 경우
        for i in range(len(s)):
            if s[i] == '.': # 만약 3.14일경우 .앞에 있는것만 반환하기위헤 break
                break
            else:
                if ord(s[i]) == 45 or ord(s[i]) == 43: # +와-
                        res += s[i]
                if ord(s[i]) >= 48 and ord(s[i]) <= 57: # 숫자들
                    res += s[i]   
                else:
                    pass
        return(res) # 결과 프린트
else:
    return(0) # 아닐시 0 출력
```
---
這是我第一次只用ascii去處理的程式碼，但他會跳出index out of range的 error 目前還在想....\
도대체 왜 index out of range error가 나오는지 모르겠다....
