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
r = re.compile('^a')
m = r.search('abbc')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 1), match='a'>
a 0 1 (0, 1)
```



#### {숫자}기호 _문자에 해당 기호를 붙이면, 해당 문자를 숫자만큼 반복한다

```python
r = re.compile('av{2}c')
m = r.search('abbc')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 4), match='abbc'>
abbc 0 4 (0, 4)
```



#### {숫자1,숫자2}기호

- 문자에 해당 기호를 붙이면, 해당 문자를 숫자1이상 숫자2이하만큼 반복한다
- 반복 횟수를 고정할때 사용한다

```python
# b가 2개이상 4개이하로 반복시킨다
r = re.compile('ab{2,4}c')
m = r.search('abbc')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 4), match='abbc'>
abbc 0 4 (0, 4)
```



#### {숫자,}기호 _문자에 해당 기호를 붙이면 해당 문자를 숫자 이상만큼 반복한다

```python
# a가 2이상이어야한다
r = re.compile('a{2,}bc')
m = r.search('aaabc')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 5), match='aaabc'>
aaabc 0 5 (0, 5)
```



#### {,숫자}기호 _문자에 해당 기호를 붙이면 해당 문자를 숫자 이하만큼 반복한다

```python
# b가 4개이상이면 오류뜬다
r = re.compile('ab{,3}c')
m = r.search('abbbc')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 5), match='abbbc'>
abbbc 0 5 (0, 5)
```



#### [_]기호 _문자클래스 기호 [.]안에 문자들을 넣으면 그 문자들 중 한개의 문자와 매치한다는 의미이다

```python
r = re.compile('[abc]')
# 최초 일치하는 문자 b를 가져온다
m = r.search('baaca')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 1), match='b'>
b 0 1 (0, 1)

# 최초 일치하는 문자 b를 가져온다
m = r.match('baaca')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 1), match='b'>
b 0 1 (0, 1)
```

```python
# a~z까지 포함
r = re.compile('[a-z]')
m = r.findall(' 3 life is to short')
print(m)

> ['l', 'i', 'f', 'e', 'i', 's', 't', 'o', 's', 'h', 'o', 'r', 't']

r = re.compile('[a-z]+')
m = r.findall('life is to short')
print(m)

> ['life', 'is', 'to', 'short']
```



#### [^문자] 기호_ ^기호 뒤에 붙은 문자들을 제외한 모든 문자를 매치하는 역할을 한다

```python
r = re.compile('[^abc]')
# abc가 아닌 k가 와서 오류가 안뜬다
m = r.search('korea')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 1), match='k'>
k 0 1 (0, 1)
```



### 정규 표현식 모듈함수

#### split() _입력된 정규 표현식을 기준으로 문자열들을 분리하여 리스트로 리턴. 자연어처리에 가장많이 사용되는 정규 표현식중 하나. 토큰화에 유용

```python
text = '''사과
딸기
수박
멜론
바나나'''

m = re.split('\n', text)
print(m)

> ['사과', '딸기', '수박', '멜론', '바나나']

text = '사과+딸기+수박+멜론+바나나'
# 그냥 +만 넣게 되면 오류발생
m = re.split('\+', text)
print(m)

> ['사과', '딸기', '수박', '멜론', '바나나']
```

```python
text = '''
이름 : 홍길동
전화 번호 : 010- 1234- 5678
나이 : 30
성별 : 남
'''

# r = re.compile('[0123456789]+')
# r = re.compile('[0-9]+')
r = re.compile('\d+') # \d는 숫자를 의미한다

m = r.findall(text)
print(m)
> ['010', '1234', '5678', '30']

# 숫자가 아닌것만 가져온다
r = re.compile('\D+')
-> 소문자와 대문자를 주의해야한다
```



#### r.sub() _정규 표현식 패턴과 일치하는 문자열을 찾아서 다른 문자열로 대체하는 함수이다

```python
r = re.compile('blue')
# r. sub('바꿀 문자열', '대상 문자열')
m = r.sub('color', 'blue socks and red shoes')
print(m)

> color socks and red shoes

r = re.compile('blue|red|green')
m = r.sub('color', 'blue socks and red shoes')
print(m)
print(type(m))

> color socks and red shoes
<class 'str'>
```



#### subn() _sub() 비슷하지만 리턴은 튜플로 한다

```python
r = re.compile('blue|red|green')

m = r.subn('color', 'blue socks and red shoes')

print(m)

> ('color socks and color shoes', 2)
```



#### 정규 표현식 텍스트 전처리

```python
text = """
100 John   PROF
101 James  STUD
102 Mac    STUD
"""

m = re.split('\s+', text)
print(m)

> ['', '100', 'John', 'PROF', '101', 'James', 'STUD', '102', 'Mac', 'STUD', '']

r = re.compile('\d+')
m = r.findall(text)
print(m)

> ['100', '101', '102']

r = re.compile('[A-Z]{4}')
m = r.findall(text)
print(m)

> ['PROF', 'STUD', 'STUD']

m = re.findall('[A-Z][a-z]+', text)
print(m)

> ['John', 'James', 'Mac'] 
```



### 컴파일 옵션 _정규식을 컴파일할 때 사용하는 옵션이다

```python
r = re.compile('a.b', re.S) # re.DOTALL의 축약은 re.S이다
m = r.match('a\nb')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 3), match='a\nb'>
a
b 0 3 (0, 3)

# 대소문자에 관계없이 매치할수 있도록 한다
# r = re.compile('[a-zA-Z]')

r = re.compile('[a-z]', re.I) # re.IGONRECASE
m = r.match('Life is to short')
print(m)

> <re.Match object; span=(0, 1), match='L'>
```

```python
# 여러 줄과 매치할 수 있도록 한다
r = re.compile('^python\s\w+', re.M) # re.MULTILINE

data="""python one
life is too short
python two
you need python
python three"""

m = r.findall(data)
print(m)

> ['python one', 'python two', 'python three']
```

```python
# ( ) 의 의미도 그룹으로 묶어준다 | 은 or을 의미한다
r = re.compile('&#(0[0-7]+|[0-9]+|x[0-9a-fA-F]);')

data = '''&#06;
&#09;
&#xa;'''

m = r.findall(data)

print(m)

> ['06', '09', 'xa']
```



#### 백슬래시 (\)

```python
r = re.compile('\section') # \c \w \s:공백

m = r.match(' ection')
print(m)

> <re.Match object; span=(0, 7), match=' ection'>
```



### 문자열 소모가 없는(zero-with assertions) 메타문자

#### | 메타문자는 or과 동일하다

```python
r = re.compile('Crow|Servo')
m = r.match('CrowHello')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 4), match='Crow'>
Crow 0 4 (0, 4)
```



#### ^메타문자는 문자열의 맨 처음과 일치함을 의미한다

```python
r = re.compile('^Life')
m = r.match('Life is too short')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(0, 4), match='Life'>
Life 0 4 (0, 4)
```



#### $메타문자는 ^메타문자와 반대인 경우이다 즉, $메타문자는 문자열의 끝과 매치해야한다

```python
r = re.compile('short$')
#m = r.match('short')
m = r.search('Life is too short')
print(m)
print(m.group(), m.start(), m.end(), m.span())

> <re.Match object; span=(12, 17), match='short'>
short 12 17 (12, 17)
```



#### \A메타문자는 ^메타문자와 같은 의미이다 하지만 re.MULTILINE \A 메타문자는 전체 문자열의 처음과 매치되지만 ^메타문자는 라인별(문단별)문자열의 처음과 매치됨을 의미한다

```python
r = re.compile('\Apython', re.M)

data="""python one
life is too short
python two
you need python
python three"""

m = r.findall(data)
print(m)

> ['python']
```

```python
r = re.compile('^python', re.M)

data="""python one
life is too short
python two
you need python
python three"""

m = r.findall(data)
print(m)

> ['python', 'python', 'python']
```



\Z는 문자열의 끝과 매치됨을 의미한다 re.MULTLINE 옵션을 사용할 경우 $메타 문자와는 달리 전체 문자열의 끝과 매치된다

```python
r = re.compile('python$', re.M)

data="""python one
life is too short
python two
you need python
python three python"""

m = r.findall(data)
print(m)

> ['python', 'python']
```

```python
r = re.compile('python\Z', re.M)

data="""python one
life is too short
python two
you need python
python three python"""

m = r.findall(data)
print(m)

> ['python']
```



#### \B메타문자는 \b메타문자와 반대의 경우로 whitespace로 구분된 단어가 아닌 경우에만 매치된다

```python
r = re.compile('\Bclass\B')
m = r.findall('the declassified algorithm')
print(m)

> ['class']
```



### 그룹핑

- 문자열이 계속해서 반복되는지 조사하는 정규식

- () : 그룹을 만들어 주는 메타문자이다

  |     group(인덱스) |             설명              |
  | ----------------: | :---------------------------: |
  | group(0), group() |      매치된 전체 문자열       |
  |          group(1) | 첫번째 그룹에 해당하는 문자열 |
  |          group(2) | 두번째 그룹에 해당하는 문자열 |
  |          group(n) | n번째 그룹에 해당하는 문자열  |

```python
r = re.compile(r'(\w+)\s+((\d+)-\d+-\d+)') # 왼쪽 -> 오른쪽, 바깥 -> 안으로

m = r.search('park 010-1234-5678')
print(m)
print(m.group())
print(m.group(0))
print(m.group(1))
print(m.group(2))
print(m.group(3))

> <re.Match object; span=(0, 18), match='park 010-1234-5678'>
park 010-1234-5678
park 010-1234-5678
park
010-1234-5678
010
```



전방탐색

```python
r = re.compile('.+:')
m = r.search('http://google.com')
print(m)

> <re.Match object; span=(0, 5), match='http:'>
```

```python
# ':' 앞에 있는 문자열만 가져오기
# ?= 긍정형 전방탐색을 이용해서 http만 가져온다
# (?=...) : ...정규식과 매치되어야 하며 조건이 통과되어도 문자열이 소멸되지 않는다
r = re.compile('.+(?=:)')
m = r.search('http://google.com')
print(m)

> <re.Match object; span=(0, 4), match='http'>
```



부정형 전방탐색

```python
# ?! 부정형 전방탐색을 이용해서 http만 가져온다
# (?!...) : ...정규식과 매치되지 않아야 하며 조건이 통과되어도 문자열이 소멸되지 않는다

r = re.compile('.+(?!:)')
m = r.search('http://google.com')
print(m)

> <re.Match object; span=(0, 17), match='http://google.com'>
```



#### Greedy vs Non-Greedy

```python
# *메타문자는 매우 탐욕스러워서 매치할 수 있는 최대한의 문자열을 모두 소모시킨다
r = re.compile('<.*>')
m = r.match('<html><head><title>Title</title>')
print(m.group())
len(m.group())

> <html><head><title>Title</title>
32
```

```python
# *메타문자의 탐욕을 제한할 수 있도록 Non-Greedy 문자인 ?을 사용한다
# Non-Greedy문자인 ?은 *?, +?, ??, {m,n}? 과 같이 사용한다
# 가능한 가장 최소한의 반복을 수행하도록 도와주는 역할을 한다

r = re.compile('<.*?>')
m = r.match('<html><head><title>Title</title>')
print(m.group())
len(m.group())

> <html>
6
```

