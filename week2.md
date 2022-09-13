# 2022.09.13(화)

# [Python][프로그래머스 Lv.2] 괄호 변환

### 나의 풀이
```Python
def correct(s):
    a = 0
    b = 0
    arr = list(s)
    for i in arr:
        if i =='(' and a >= b:
            a += 1
        elif i == ')' and a >= b:
            b += 1
        else:
            return False
    if a == b:
        return True
    else:
        return False

def solution(p):
    answer = ''
    a = 0
    u = ''
    v = ''
    tmp=''
    if correct(p) or len(p)==0:
        return p
    arr = list(p)
    for i in range(len(arr)):
        if arr[i] == '(':
            a += 1
        else: 
            a -= 1
        if a == 0:
            u = p[0:i+1]
            v = p[i+1:]
            break
    if correct(u):
        return u + solution(v)
    else:
        tmp += '('
        tmp += solution(v)
        tmp += ')'
        for c in u[1:len(u)-1]:
            if c == '(':
                tmp += ')'
            else:
                tmp += '('
    return answer + tmp
```
// correct(): 올바른 괄호 문자열인지 확인    
correct()는 옛날에 풀었던 올바른 괄호 문제에서 그대로 가져온 코드이다.

문제가 지시하는 순서대로 코드를 작성했다.

 

1. 주어진 문자열이 올바른 괄호 문자열이거나 빈 문자열이면 그대로 반환(return)
2. 주어진 문자열을 균형잡힌 문자열 u와 나머지 문자열 v로 나누어 반환
3. u가 올바른 문자열이면, 1로 돌아가 v에 대해 수행한 후 u에 그 결과를 더해줌(return)
4. u가 올바른 문자열이 아니면, 1로 돌아가 v에 대해 수행한 결과를 '('와 ')' 사이에 넣고
첫 번째 문자, 마지막 문자를 제거한 u에 대해 괄호 방향을 반대로 바꿔줌
5. 4에서 수행한 결과를 return


예를 들어,     
"()))((()"의 경우 위의 순서대로 수행하면 다음과 같다.    
u = "()"     
v = "))((()"      
answer = u + solution("))((()")      

u = "))(("      
v = "()      
answer = "(" + solution("()") + ")" + "()"       
// 마지막에 더해지는 괄호 문자열: 첫 번째 문자, 마지막 문자를 제거한 u에 대해 괄호 방향을 반대로 바꿔준 것      

answer = "()"      

여기서 return되면 answer = "()" + "(" + "()" + ")" + "()" 이다.     
따라서, 결과는 "()(())()"가 나온다.     
 

### 다른 사람의 풀이
```Python
def solution(p):
    if p=='': return p
    r=True; c=0
    for i in range(len(p)):
        if p[i]=='(': c-=1
        else: c+=1
        if c>0: r=False
        if c==0:
            if r:
                return p[:i+1]+solution(p[i+1:])
            else:
                return '('+solution(p[i+1:])+')'+''.join(list(map(lambda x:'(' if x==')' else ')',p[1:i]) ))
```
lambda를 써보는 연습을 해봐야겠다..