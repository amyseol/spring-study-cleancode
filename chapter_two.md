# 2장_의미 있는 이름

### 1. 의도를 분명히 하기 <br/>
의도가 드러나는 이름은 코드 이해도를 높이고 변경이 쉬워진다. <br/>
변수, 함수, 클래스의 존재 이유, 수행 기능, 사용 방법 을 이름으로 답할 수 있어야 한다.

#### ► 경과 시간을 날짜로 표현하는 이름
- int elapsedTimeInDays; <br/>
- int daysSinceCreation; <br/>
- int daysSinceModification; <br/>
- int fileAgeInDays; <br/>

표현하려는 개념에 이름만 붙여도 코드가 상당히 나아진다.

#### ► 지뢰찾기 게임
- gameBoard라는 2차원 배열을 반복하면서 각 셀을 확인한다.
- 셀(cell) 의 상태(STATUS_VALUE)가 깃발이 꽂힌 (FLAGGED) 상태가 되면 해당 셀을 flaggedCells 리스트에 추가한다.
  ```java
  	public List<int[]> getFlaggedCells(){
  		List<int[]> flaggedCells = new ArrayList<int[]>();
  		for (int[] cell : gameBoard)
  			if(cell[STATUS_VALUE]==FLAGGED)
  				flaggedCells.add(cell);
  		return flaggedCells;
  	}
  ```
- int 배열 대신 칸을 Cell 이라는 클래스로 만들고, isFlagged() 라는 함수를 사용해 FLAGGED 라는 상수를 감출 수 있다.
  ```java
   public List<**Cell**> getFlaggedCells(){
  		List<Cell> flaggedCells = new ArrayList<int[]>();
  		for (Cell cell : gameBoard)
  			if(cell.**isFlagged()**)
  				flaggedCells.add(cell);
  		return flaggedCells;
  	}
  ```

### 2. 그릇된 정보는 피하기 <br/>
널리 쓰이는 의미가 있는 단어를 사용하지 않는다. <br/>
- 계정을 담는 컨테이너 실제 List가 아니라면 accountList 라고 명명하면 안된다.  <br/>
  accountGroup, bunchOfAccounts, Accounts 등으로 명명해야 한다. 
- 서로 흡사한 이름을 사용하지 않도록 주의한다.<br/>
  한 모듈에서 AccountControllerForFlaggedGameOfKorea 라고 쓰고,  <br/>
  다른 모듈에서 AccountControllerForGameGuidelineOfKorea 라고 쓰면 안된다. 너무 비슷하다.
- 소문자 L 이나 대문자 O 를 사용하지 않는다. 숫자 0 이나 1 과 헷갈릴 수 있다.

### 3. 의미 있게 구분하기
같은 이름에 연속적인 숫자만 덧붙이거나 (a1, a2, a3,…) 불용어를 추가하지 말자. <br/>
(불용어란 문장 내에서 빈번하게 발생하여 의미를 부여하기 어려운 단어들을 의미한다. 예를 들어 a, an, the 등이 있다.) <br/>
클래스 이름을 ProductInfo 혹은 ProductData 라고 한다면 개념을 구분하지 않고 이름만 다르게 지은 것이다. <br/>
moneyAmount 와 money / customerInfo 와 customer / accountData 와 account 등의 이름은 서로 구분이 안된다.

### 4. 발음하기 쉬운 이름 사용
지적인 대화가 가능해진다. <br/>
private Date genymdhms; 보다는 private Date generationTimestamp; 를 사용하자!

### 5. 검색하기 쉬운 이름 사용
이름을 의미 있게 지으면 함수가 길어지지만 찾기가 쉬워진다.
- 아래 코드에서 다른 건 배제하고 4, 5 만 생각해보자 무엇을 의미하는지 알 수 없고 4, 5 를 검색해서는 원하는 상수를 가려내기 힘들다.
  ```java
  for(int j=0; j<34; j++){
  	s += (t[j]*4)/5;
  }
  ```
- 아래처럼 이름을 지으면 검색이 쉬워진다.
  ```
  int realDaysPerIdealDay = 4;
  int WORK_DAYS_PER_WEEK = 5;
  ```

### 6. 인코딩 피하기
유형이나 범위까지 인코딩에 넣으면 그만큼 이름을 해독하기 어렵다. <br/>
예전에는 멤버 변수에 m_ 이라는 접두어를 붙였지만, 이제는 그럴 필요가 없다. <br/>
하지만 때로는 인코딩이 필요하다.
- ABSTRACT FACTORY 구현 인터페이스 클래스와 구현할 구체 클래스(concrete class)가 필요하다.  <br/>
인터페이스 클래스를 구분하기 위해 IShapeFactory 라고 하는 것보다는  <br/>
차라리 구현 클래스를 ShapeFactoryImp 또는 CShapeFactory라고 하는 것이 낫다.

### 7. 자신의 기억력 자랑하지 말기
루프 범위가 아주 작고 다른 이름과 충돌하지 않는다면 반복 횟수를 세는 i, j, k 는 사용해도 괜찮다. (l 은 절대 안된다!)

- 클래스 이름 (객체 이름) <br/>
명사나 명사구가 적합하다. 동사는 사용하지 않는다. <br/>
좋은 예 : Customer, WikiPage, Account, AddressParser <br/>
나쁜 예 : Manager, Processor, Data, Infor

- 메서드 이름
동사나 동사구가 적합하다. <br/>
좋은 예 : postPayment, deletePage, save <br/>
접근자(Accessor), 변경자(Mutator), 조건자(Predicate)는 javabean 표준에 따라 값 앞에 get, set, is를 붙인다.
  ```java
  	String name = student.getName();
      customer.setName("amy");
      if(payment.isChecked())...
  ```
생성자를 중복 정의(overload)할 때는 정적 팩토리 메서드를 사용한다. 메서드는 인수를 설명하는 이름을 사용한다.
  ```java
  	Complex fulcrumPoint = Complex.FromRealNumber(23.0);
      // 아래 코드가 더 좋다. 
      Complex fulcrumPoint = new Complex(23.0);
      // 생성자 사용을 제한하려면 생성자를 private로 선언한다. 
  ```

### 8. 기발한 이름 피하기
너무 독창적인 이름보다는 의도가 명료한 이름을 지어야 한다.

### 9. 한 개념에 한 단어 사용
똑같은 메서드를 클래스마다 다르게 부르면 혼란스럽다. 메서드 이름은 독자적이고 일관성이 있어야 한다. <br/>
한 단어를 두 가지 목적으로 사용하면 안된다. ‘일관성’을 고려해 add 라는 단어를 선택하고 모든 add 메서드가 기존 값을 더하여 새로운 값을 만든다고 가정한다면, 집합에 값 하나를 추가하는 새로운 메서드를 add 라고 불러서는 안된다. insert 나 append 라는 이름이 적당하다.

### 10. 해법 영역에서 가져온 이름 사용
전산 용어, 알고리즘 이름, 패턴, 수학 용어 등을 사용해도 된다.
- VISITOR 패턴을 따서 AccountVisitor

### 11. 문제 영역에서 가져온 이름 사용
문제 영역 개념과 관련이 깊은 코드라면 문제 영역에서 이름을 가져와야 한다.  <br/>
코드를 읽는 프로그래머가 해당 분야 전문가에게 의미를 물어 파악할 수 있다.

### 12. 의미 있는 맥락 추가하기
마지막 수단으로 접두어를 붙인다.
- 변수 firstName, street, houseNumber, city, state 를 보면 주소라는 사실을 알 수 있지만, 메서드가 state 라는 변수만 사용한다면 주소라고 알아채기 힘들다. <br/>
주소라는 의미의 addr 접두어를 추가해 addrFirstName, addrStreet, addrState 으로 변경하면 더 명확해진다.
- 맥락이 분명한 변수
  ```java
  public class GuessStatisticMessage {	
  	private String number;
  	private String verb;
  	private String pluralModifier;
  	
  	public String make(char candidate, int count) {
  		createPluralDependentMessageParts(count);
  		return String.format("There %s %s %s%s", 
  				verb, number, candidate, pluralModifier);
  	}
  
  	private void createPluralDependentMessageParts(int count) {
  		if (count == 0) {
  			thereAreNoLetters();
  		} else if (count == 1) {
  			thereIsOneLetter();
  		} else {
  			thereAreManyLetters(count);
  		}
  	}
  
  	private void thereAreManyLetters(int count) {
  		number = Integer.toString(count);
  		verb = "are";
  		pluralModifier = "s";
  	}
  
  	private void thereIsOneLetter() {
  		number = "1";
  		verb = "is";
  		pluralModifier = "";
  	}
  
  	private void thereAreNoLetters() {
  		number = "no";
  		verb = "are";
  		pluralModifier = "s";
  	}
  }
  ```
### 13. 불필요한 맥락 없애기
Gas Station Deluxe 라는 애플리케이션을 만든다고 해서 모든 클래스 이름을 GSD로 시작하는 것은 안된다. <br/>
의미가 불분명하고 불필요한 맥락의 GSD 는 제외하자! <br/>
accountAddress 와 customerAddress 는 Address 클래스의 인스턴스로는 좋은 이름이지만, 클래스 이름으로는 적합하지 않다.

## 결론
코드를 처음 읽는 사람도 이해하기 쉽도록 명명한다. <br/>
변수, 클래스, 함수 이름은 의미를 분명하게 한다. <br/>
널리 쓰이는 단어는 피하고 비슷하게 짓지 않는다. <br/>
검색하기 쉽고 발음하기 쉽게 짓는다. <br/>
메서드 이름은 독자적이고 일관성있게 짓는다.
