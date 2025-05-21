# [스프린트] Part 1 

## 2025-05-08:
- 개강일. OT 진행
- 앞으로 7개월 동안 개인적으로 열심히 풀어나갈 [프로그래머스](https://programmers.co.kr/).
- 학부에서 **C와 C++** 위주로 공부했기 때문에 이번 기회에 파이썬에 열심히 적응을 해볼 예정.
- **pythonic**한 코드에 집중할 예정
- 또한 한 가지 원칙은 이 페이지에는 **인용 문구 없이 챗GPT를 절대로 사용하지 않을것**. 오로지 나의 생각과 정리를 위해서 페이지를 사용할 것이며 참고를 위한 GPT 인용은 가져올 것임.
#### 
---
## 2025-05-09:
- `list comprehension` 파이썬에서 pythonic한 코드를 짜는 방식이 왜 좋은가?
   - **"명료함이 복잡함보다 낫다"** 에 따라, 코드는 직관적이고 쉽게 읽힐 수 있어야 합니다. (아직 직관적이진 않음음)
```python
# 비 Pythonic
numbers = [1, 2, 3, 4, 5]
squared = []
for n in numbers:
    squared.append(n ** 2)

# Pythonic
squared = [n ** 2 for n in numbers]
```

- python의 강력한 내장함수는 가독성이 높고 효율적인 코딩이 가능하다는 점에서 **pythonic**하다.
```python
# 비 Pythonic: 반복문으로 문자열 연결
result = ""
for word in words:
    result += word

# Pythonic: 내장함수 join() 사용
result = "".join(words)
```
- `enumerate`는 더 pythonic한 코드라고 한다. (why?)
```python
# 비Pythonic
for i in range(len(my_list)):
    print(i, my_list[i])

# Pythonic
for i, val in enumerate(my_list):
    print(i, val)
```
---
## 2025-05-12: 
- 마크다운 파일 만들어서 로컬에서 pull하고 vscode 기반에서 push까지

- N이하의 소수의 합 구하기(에르토스테네스의 체로 optimization)
  최적화 이슈를 만났을때 당황하지 않기.

## 2025-05-13
`greedy 알고리즘` 주어진 시간에서 최적의 할일 찾기.

## 2025-05-14


## 2025-05-15
- 클래스의 생성자(__init__메소드)는 **명시적으로 리턴 타입을 지정해주지 않아도** 객체를 반환하도록 설계되어있다
- 문자열을 ("")로 초기화하는 건 위험하다. None을 쓰는 것이 더 pythonic


## 2025-05-16
#### **< 실습과제 > Hotel Booking Demand Datasets 분석해보기(EDA) from 캐글**
- data analysis에서 입문용으로 많이 사용하는 데이터셋(csv타입)
- pandas의 DataFrame을 사용하면 numpy나 list보다 조금 더 유연하게 사용이 가능하다



- pandas의 DataFrame을 다룰때 아주 효율적인 `fillna()` 메th드는 결측치를 처리하는데 효과적이지만 가끔 경고가 뜨기도 하는데 `SettingWithCopyWarning`의 경우다.

```
players_df.loc['Ben Davies', :].fillna(29, inplace=True)
```

이 부분이 **Ben Davies 행의 복사본**을 반환할 가능성이 있다는 것 때문
Pandas는 loc[row_label, :]으로 선택한 결과를 **반드시 원본의 뷰(view)** 로 보장하지 않는다고 한다(...)

`df.loc[:, col] = ...`	
근데 위와 같은은 컬럼 단위의 수정은 경고 없이 안정적이라고 한다;;

(이럴거면 뭐하러 만들어놓은겨 헷갈리게...)


## 2025-05-19
#### matplotlib vs Seaborn
`matplotlib` 기반으로 만들어진 라이브러리. 간편하게 근사한 그래프 생성하고 싶다면 `Seaborn` 추천
(Seaborn은 아직 사용해보지 않아서 한번 해봐야겠음!)

> ChatGPT의 생각이 궁금해서 물어봤더니

| 용도               | 추천 도구                                |
| ---------------- | ------------------------------------ |
| EDA / 초안 시각화     | `Seaborn` or `Altair`            |
| 논문 최종 제출용        | `Matplotlib (pgf backend)` + 수동 조정 |
| R 사용자라면          | `Plotnine`                             |
| LaTeX 완벽 통합 원할 때 | `TikZ` / `pgfplots`                      |


#### Pd.df.loc
Pandas의 DataFrame을 사용할때 `iloc`과 `loc`을 이용해서 인덱싱을 많이 하는데 `loc`의 경우는 DataFrame에서 바로 인덱싱을 해도 되지만 더 폭 넓은 인덱싱이 가능했다.

예를 들면
```python
df['company':'agent'] # 접근 안됨

df.loc['company':'agent'] # 마치 numpy처럼 인덱싱이 가능
```

#### Seaborn의 heatmap
Seaborn에서 사용할만한 함수는 Boxplot과 heatmap함수일 것 같다.
```python
sns.heatmap(df.corr(), annot=true)
```
`sns.heatmap()` 함수의 경우 df를 그대로 넣는 것이 아니라 correaltion을 구한 다음에 넣는다는 것이 포인트.

#### Pandas DataFrame 주요 메서드 및 변수
개인적으로 pandas는 굳이 사용할 일이 없었는데, 다루는 데이터가 DataFrame이 아니다보니 쓸일이 아예 없었다. 그러나 데이터 사이언스 관점에서는 동일한 과정이 진행되기 때문에 한번 공부해보는 것이 좋다고 판단되어 정리를 해보았음.
`df.describe()`
`df.info()`
`df.shape`
`df.dtype()`
`df.rename()`: column명을 바꿀때 사용하곤 한다
`df.drop(columns='')`: 해당 데이터 삭제. 기본적으로 row 삭제. 그러나  column도도 삭제 가능
`df.isna().any(axis=1)`: 결측값이 있는 row를 bool인덱싱할때 유용하다.
`df.dropna()`: 결측치 있는 데이터 삭제. 그러나 데이터를 삭제한다는 것은 신중하게 해야하므로 확신이 있을때 사용.
`df.fillna()`: 결측치가 있는 데이터를 보완하기 좋음!
`df.duplicated()`: 중복된 데이터 찾기. df.duplicated().sum()
df.duplicated(subset='컬럼명', keep='last')
`df.drop_duplicates()`: 중복값 삭제
`df.unique()`:유일한 값을 뽑아낼때 유용
`df.astype()`: data type 설정
`df.value_counts(dropna=False, normalize=True)`
`df.str`: 문자열 처리

- 다만 DataFrame과 Series는 각각 적용될 수 있는 함수가 다르다. 즉, 그때 그때 잘 찾아봐라...(중요하진 않음)



## 2025-05-20
### 왜 AI 엔지니어는 선형대수를 배워야하는가?
수업 시간에 나왔던 질문이었는데 나름 정리가 잘 되어있다고 생각했지만 강사님이 버벅이는거 보고 나도 다시 한번 정리해야겠다는 생각이 들었다.

#### 우리가 다루는 데이터에 접근하기 위함
일단 딥러닝에 한해서 답변을 생각해보면 결국 우리가 다루는 데이터가 핵심일 것이다. 딥러닝은 데이터를 통해서 학습을 시키기 때문에 해당 데이터에 접근해야하는데, 우리가 다루는 데이터(사진, 음성, 고차원 신호)를 들여다 보면 결국 어떤 엔지니어가 설계했을 것이고 데이터에 접근하는 방식은 직관적일것이다. 미치지 않고서야 데이터의 값을 별 인간이 이해하지 못하게 설계하진 않았겠지. 아무튼 너무 당연한 현상을 길게 풀어쓰려다보니까 말이 약간 꼬였는데 **데이터의 값에 접근하는 것은 인간의 사고를 벗어나지 않는 직관적인 방식**이라는 것이 포인트.

#### 딥러닝 모델도 선형적인 모델이 최선
신기하게도 딥러닝의 가장 작은 단위인 뉴런도 선형적인 모델을 사용하고 있다(물론 activation function까지 포함한 비선형적인 형태로 존재하지만). 그럼 뉴런의 구조가 2차,3차식이나 sin이나 복잡한 비선형 구조를 쓰면 안되는가?에 대한 의문이 들었고 이건 많은 연구자들이 이미 고민을 했을 부분일 것이다. 그런데 왜 안됐을까? 이건 당연히 구현이 안되거나, 구현을 해도 비효율적이여서 그랬을 것이다. sin이나 여러 비선형 함수는 직관적이지도 않을뿐더러 학문적 뿌리도 없고 무엇보다 backpropagation을 어떻게 구현할것인가? 답이 없다. 그럼 차수가 2,3인 구조는? backpropagation까지는 가능하겠지만 늘어나는 연산량에 비해서 정보가 주는 효율성이 없다. 주어진 데이터는 한정적인데 그걸 제곱한다고 한들 어떤 유의미한 결과를 낼 수 있을까? 아마 overfitting 되는 결과만 초래했을 것이다.

#### 결론은
데이터도 그렇고 딥러닝의 모델도 그렇고 우리는 결국 선형적인 데이터와 모델을 통해서 지금 시대의 딥러닝 기술까지 오게 된것이다. 모든 엔지니어의 목표인 비선형적인 시스템을 구축하는 것을 딥러닝이라는 방식으로 구현이 되었으며 이것이 인공지능이라는 분야가 발전해온 역사와 백그라운드에 대한 이해 없이는 답을 하기가 매우 어렵다는 사실을 느꼈다.
