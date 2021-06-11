### pivot

- 각 컬럼의 값을 교차테이블 구성요소로 전달, 교차테이블 완성
- index, columns, valuse 컬럼을 각각 전달
- 요약기능 없음
- dataframe.pivot(index, columns, values)

```python
# inplace = True 를 설정하면, 실제 데이터에 변경사항이 적용된다.
krecom_pivot.fillna(0, inplace=True)
```



### pivot_table

- pivoit 기능과 유사, 더 많은 옵션 사용 가능
- index, columns, values 컬럼을 각각 전달
- aggfunc 옵션 사용하여 요약 기능 전달 가능(기본은 평균)
- fill_value 옵션 사용하여 NA값 대체 가능
- dataframe.pivot_table(index, columns, values, aggfunc='mean', fil_value)

