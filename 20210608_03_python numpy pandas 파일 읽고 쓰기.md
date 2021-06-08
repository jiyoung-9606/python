### 파일

- 2가지 종류의 파일 형태
  - 사람기준(txt)
  - 기계기준(binary)

### python

```python
%%writefile padsample/gosu.txt
hello
안녕
>Overwriting pdsample/gosu.txt
```

'wb'는 write + binary의 줄임표현이다.
쓰기모드로 파일을 불러오며, binary로 저장한다는 의미이다.

```python
a = open('pdsample/gosu2.txt','wb')
```



### with

with 구문은 시작할 때 enter를, 종료할 때 __ exit를 자동으로 실행해준다. exit가 실행되었기 때문에 close()를 안해준다. with가 끝난 후 write()하면 'write to closed file'에러가 발생한다.

```python
with open('pdsample/gosu4.txt', 'w') as c:
    c.write('안녕하세요?\n')
    c.write('파이썬\n')
with open('pdsample/gosu4.txt') as c:
    print(c.read())
>안녕하세요?
파이썬
```



### numpy

numpy 자체적으로 저장과 불러오는 기능을 지원한다.

```python
# t.npy로 저장된다.
# array객체 하나는 save()로 저장할 수 있다.
# 확장자는 자동으로 npy가 붙는다.
np.save('pdsample/t', a)
numpy의 데이터를 파일에 저장한다.

# 읽어올 때는 npy확장자를 붙여서 읽어와야 한다.
# b = np.load('pdsample/t') 확장자없이 불러오면 오류발생
b = np.load('pdsample/t.npy')
b
>array([0, 1, 2, 3, 4])
numpy의 파일을 읽어온다.
```



### pandas

```python
import pandas as pd
a = pd.read_csv('pdsample/num.txt', header=None)
a
# pandas 의 DataFrame 파일에 저장
a.to_csv('pdsample/num2.csv', sep=',')
```

