![문제](./problem.png)

## 내 생각
십의 자리 소수(2,3,5,7)을 이용하여 n의 자리수를 조합하여 소수인지 판별한다.
에라토스테네스의 체를 이용하여 소수인지 판별


```python
n=int(input())

# 소수 판별
def isPrime(a):
    if(a<2):
        return False
    for i in range(2,int(a**0.5)+1):
        if(a%i==0):
            return False
    return True

def dfs(num):
	# 목표 길이 도달 시 멈춤
    if len(str(num))==n:
        print(num)
    else:
        for i in range(10):
            temp=num*10+i
            if isPrime(temp):
                dfs(temp)

dfs(2)
dfs(3)
dfs(5)
dfs(7)
```

    2333
    2339
    2393
    2399
    2939
    3119
    3137
    3733
    3739
    3793
    3797
    5939
    7193
    7331
    7333
    7393

