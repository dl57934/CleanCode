# 2. 이름 정하기

### 1. 의도가 분명하게 이름을 지어라 

- 좋은 이름을 지으려면 시간이 걸리지만 좋은 이름으로 절약하는 시간이 훨씬 많다. 이점을 생각하며 이번 파트의 내용을 적어본다.

- 변수, 함수, 클래스 이름은 다음과 같은 질문에 답해야한다. 
존재 이유, 수행기능, 사용방법 따로 주석이 필요하다면 의도를 들어내지 못한 것이다. 

아래 예시를 보자

변수 
```java
//안좋은 예시
int d; //경과 시간(단위: 날짜)

//좋은 예시
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

메소드
```java
public List<int[]> getThem(){
  List<int[]> list1 = new ArrayList<int[]>();
  for (int[] x:theList)
    if(x[0] == 4)
      list.add(x);
  return list1;    
}
// 지금 보면 복잡한 것 도 없는 단순한 형태의 메소드이다. 

// 하지만 이코드에는 단순함 보다는 함축성이 문제다.  
// 각 변수들이 무엇을 의미하며 4는 무슨 의미인지 결론적으로 이메소드는 무슨 역활을 하는지 알아보기 힘들다. 

// 위의 코드를 지뢰찾기 게임에 쓰인다고 생각하여 코드를 바꿔보겠다. 

public List<int[]> getFlaggedCells(){
  List<int[]> flaggedCells = new ArrayList<int[]>();
  for(int[] cell: gameBoard)
    if(cell[STATUS_VALUE] == FLAGGED)
      flaggedCells.add(cell);
    return flaggedCells;  
}
// 이 코드를 보면 들여쓰기 변수 수 돌아가는 로직은 같은데 상수와 변수의 이름을 바꾸어 남들이 봤을때 조금 더 명확한 코드가 되었습니다. 

public List<Cell[]> getFlaggedCells(){
  List<Cell> flaggedCelss = new ArrayList<Cell>();
  for(Cell cell: gameBoard)
    if(cell.isFlagged())
      flaggedCells.add(cell);
  return flaggedCells    
}
위의 코드는 단순히 이름만 바꾸어 줬는데 모든 기능이 확실시 되어 졌습니다.
```

### 잘못된 정보를 피하라

- 널리 쓰이는 의미가 있는 단어를 다른 의미로 사용해도 안된다. hp,aix, sco는 변수이름으로 적합하지않다. 왜냐하면 이같은 이름은 유닉스와 유닉스 변종에서 사용하고 있는 이름이기 때문이다. 
- 서로 흡사한 의미를 사용하지 않도록 주의한다. (다른 모듈들 사이에서 비슷한 변수이름을 사용하지 않는다.)
- 유사한 개념은 유사한 표기법을 사용한다. 일관성이 떨어지는 표기법은 그릇된 정보이다. 
- O, l만을 변수로 사용하지 말자 l은 1같이 보이고 O는 0같이 보이는 불상사가 발생할 수 있다. 

### 의미 있게 구분하라 

- 이름이 달라야 한다면 의미도 달라져야 한다. 
예를 들어 n1, n2, n3와 같은 방법은 외도적인 이름과 정반대이다. 
- Info와 Data는 정확히 구분되지 않는다. 
불용어는 중복이다. 
- NameString이 Name보다 뭐가 나은가? 
- Customer와 CustomerObject는 어떠한 차이가 있는가? 
- getActiveAccount(), getActiveAccounts(), getActive AccountsInfo()의 차이점을 알겠는가? 직접 뒤져보지 않는 이상 알기 힘들것이다. 

- 결론적으로 말하고 싶은건 읽는 사람이 차이를 알도록 이름을 지어라.

### 발음하기 쉬운 이름을 사용하라

아래 두 예제를 보자

```java
class DtaRcrdd102{
  private Date genymdhms;
  private Date modymdhms;
  private final String pszqint = "102";
  }
  
  class Customer{
    private Date generationTimestamp;
    private Date modificationTimestamp;
    private final String recordId = "102";
  }
```
둘째 코드는 지적인 대화가 가능해진다. 1번째 코드와 같이 이상하게 줄이지 않고 발음이 쉬워지니 다름사람들이 이해하기 쉽고 대화가 가능해진다. 

### 검색하기 쉬운 이름을 사용하라 

- 코딩을 할때 필요한 이름을 찾을 때가 있다 만약에 상수를 그냥 5라고 사용했다면 찾기 힘들 것이다 아래의 예제를 보자

``` java
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
for (int j=0; j < NUMBER_OF_TASKS; j++){
  int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
  int realTaskWeeks = (realTaskDays / WORK_DAYS_PER_WEEK);
  sum+=realTaskWeeks;
  }
  ```
 이 코드를 보면 단순히 5, 4라고 쓴것 보다 변수 이름을 붙여주니 찾기가 많이 쉬웠다. 
 - 이름 길이는 범위 크기에 비례해야한다.  

### 인코딩을 피하라

굳이 부담을 더하지 않아도 이름에 인코딩할 정보는 많다. 유형이나 범위 정보까지 인코딩에 넣으면 해독하기 어려워 진다. 
그러므로 인코딩 언어까지 배우라는건 개발자에게 힘들어진다. 

1. 헝가리식 표기법 

이는 변수의 타입에 맞추어 접두어를 붙이는 것이다. 

byte, boolean면 b
int, short면 n 
long이면 l을 접두엉에 붙여서 사용하는 방식이다. 

당시에는 컴파일러가 타입을 점검하지 않았으므로 프로그래머에게 타입을 기억할 단서가 필요했다. 
하지만 요즘에는 컴파일러가 타입을 기억하고 강제한다. 그러므로 이제는 사용할 필요가 없는 방식이다. 

2. 인터페이스 클래스와 구현 클래스 

때로는 인코딩이 필요한 경우도 있다. 

ShapeFactory

인터페이스 ShapeFactoryImp
클래스 ShapeFactory

### 자신의 기억력을 자랑하지 마라 

- 코드를 읽으면서 변수 이름을 자신이 아는 이름으로 변환해야 한다면 그 변수 이름은 바람직하지 못하다. 
- 변수명이 한글자인건 반복문을 제외하고는 사용하지 않는다. 
- 명료함이 최고라는 사실을 이해한다. 

### 클래스 이름

- 클래스 이름과 객체 이름은 명사나 명사구가 적합하다.
Good | Bad
-----|-----
Customer|Manger
Account|Processor
AddressParser|Data

### 메소드 이름
- 메소드 이름은 동사나 동사구가 적합하다. 
ex) postPayment, deletePage, save
- 접근자, 변경자, 조건자는 get, set, is 등을 붙인다. 
```java
String name = employee.getName();
customer.setName("mike");
if(paycheck.isposted())
```
- 생성자를 중복정의할때는 정정 팩토리 메서드를 사용한다. 메소드는 인수를 설명하는 이름을 적는다. 

```java
Better
Complex fulcrumPoint = Complex.FromRealNumber(23.0);

bad
Complex fulcrumPoint = new Complex(23.0);
```

### 기발한 이름은 피하자

- 자신만 알아볼 수 있거나 특정 문화건에서만 사용하는 말은 피하자!

### 한 개념에 한 단어를 사용하라 

- 추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다.
ex)
 비슷한 의미의 단어를 
- IDE에서 제공하는 메소드를 한눈에 보기 위해서는 독자적이고 일관적이어야한다. 

### 말장난을 하지마라 

- 한단어를 두가지 목적으로 사용하지 마라.
- 기존의 것과 맥락이 다르다면 다른단어를 사용해도된다.
ex) add는 둘을 더하는 기능이고 append는 배열에 값을 추가하는 기능이다. 

- 코드를 최대한 이해하기 쉽게 작성해야한다. 

### 해볍 영역에서 가져온 이름을 사용하라

- 읽을 사람이 같은 프로그래머라면 전산 용어, 알고리즘 이름, 패턴 이름 등을 사용해도 괜찮다. 
- 프로그래머가 읽으므로 익숙한 기술 개념에는 기술 이름을 쓰자. 

### 문제영역에서 가져온 이름을 사용하라 

- 적절한 프로그래머 용어가 없다면 문제 영역에서 이름을 가져온다. 

### 의미 있는 맥락을 추가하라 

- 클래스, 함수, 변수에 맥락을 부여한다. 
- 모든 방법이 실패하면 접두어를 붙인다. 
- 비슷한 변수들이 많아서 이를 하나의 클래스에 묶어도 좋다. 

```java
//bad
private void printGuessStatistics(char candidate, int count){
  String number;
  String verb;
  String pluralModifier;
  if (count == 0){
    number = "0";
    verb = "are";
    pluralModifier = "s";
   } else if(count == 1){
    number = "1";
    verb = "is";
    pluralModifier = "";
   } else {
    number = Integer.toString(count);
    verb = "are";
    pluralModifier = "s";
   }
   String guessMessage = String.format(
    "There %s %s %s%s", verb, number, candidate, pluralModifier
   );
   print(guessMessage);
  }
```

```java
//good
public class GuessStatisticsMessage{
  private String number;
  private String verb;
  private String pluralModifier;
  
  public String make(char candidate, int count){
    createPluralDependentMessageParts(count);
    return String.format(
        "There %s %s %s%s",
        verb, number, candidate, pluralModifier);
     }
     
   private void createPluralDependentMessageParts(int count){
      if(count == 0)
        thereAreNoLetters();
      else if(count == 1)
        thereIsOneLetter();
      else
        thereAreManyLetters(count);
    }
    
    private void thereAreManyLetters(int count){
      number = Integer.toString(count);
      verb = "are";
      pluralModifier = "s";
    }
    
    private void thereIsOneLetter(){
      number="1";
      verb="is";
      pluralModifier="s";
    }
    
    private void thereAreNoLetters(){
      number="no";
      verb="are";
      pluralModifier="s";
    }
 }
 ```
 ### 불필요한 맥락을 없애라 
 
 - 고급 휘발유 충전소(Gas Station Deluxe) 어플 작성
 모든 클래스 이름을 GSD로 시작하겠다는 생각은 전혀 바람직하지 못하다. IDE에서 G를 치고 자동완성을 하면 모든 클래스를 열거할 것이다. 
 - 이름을 바꾸어야 한다. 단순하게 그냥 Address
 
 ### 마치면서
 
 -다른 사람이 질책한다고 반대할까 두려워서 그렇다고 코드르 개선할 노력을 멈추면 안된다. 
      






