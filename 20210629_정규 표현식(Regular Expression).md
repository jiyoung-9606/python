```python
import re
r = re.compile('a.c') # 정규 표현식을 컴파일 한다
m = r.search('abc') # Match라는 값으로 리턴한다 값이 같으면
print(m)
print(m.group(), m.start(), m.end(), m.span()) # span은 0에서부터 3미만의값을 가져온다

> <re.Match object; span=(0, 3), match='abc'>
abc 0 3 (0, 3)
```

### 정규식을 이용한 문자열 검색

- 컴파일된 패턴(패턴:정규식을 컴파일한 결과) 객체를 이용하여 문자열 검색을 수행하는 메소드
  - match(): 문자열의 처음부터 정규식과 매치되는지 조사
  - search(): 문자열 전체를 검색하여 정규식과 매치되는지 조사
  - findall() : 정규식과 매치되는 모든 문자열(substring)을 리스트로 리턴한다
  - finditer() : 정규식과 매치되는 모든 문자열(substring)을 반복 가능한 객체로 리턴한다



### 정규 표현식 문자

. 기호 - 한 개의 임의의 문자를 나타낸다



### ? 기호

- ? 앞의 문자가 존재할 수도 있고, 존재하지 않을 수도 있는 경우
- ? : {0,1}의미한다

```python
r = re.compile('ab?c')
m = r.search('abc')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 3), match='abc'>
abc 0 3 (0, 3)
```

```python
# match는 앞에꺼가 일치되어야한다
m = r.match('ackorea') 
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 2), match='ac'>
ac 0 2 (0, 2)
```

```python
# findall은 모든 문자가 일치하는것을 찾아줘서 list로 리턴된다
m = r.findall('ackoreaac') 
print(m)
> ['ac', 'ac']
```

```python
m = r.finditer('ackoreaac') 
print(m)
for i in m:
    print(i.group(), i.start(), i.end(), i.span())
    
> <callable_iterator object at 0x000002E50D403940>
ac 0 2 (0, 2)
ac 7 9 (7, 9)
```



#### *기호는 _바로 앞의 문자가 0개 이상일 경우를 나타낸다

```python
r = re.compile('ab*c')
m = r.search('ac')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 2), match='ac'>
ac 0 2 (0, 2)
```



#### + 기호 _*와 유사. 하지만 다른점은 앞의 문자가 최소 1개이상 이어야 한다

```python
r = re.compile('ab+c')
# b가 1번 이상은 와야된다
m = r.search('abbbc')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 5), match='abbbc'>
abbbc 0 5 (0, 5)
```



#### ^ 기호 _시작되는 글자를 지정

```python
```

