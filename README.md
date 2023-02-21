# TDD(Test Driven Development)

- #### TDD?

  테스트 주도 개발([test-driven development](http://www.incodom.kr/test-driven_development), [TDD](http://www.incodom.kr/TDD))은 소프트웨어 개발 방법론 중의 하나로, 선 개발 후 테스트 방식이 아닌 선 테스트 후 개발 방식의 [프로그래밍](http://www.incodom.kr/프로그래밍) 방법을 말한다. 다시 말해 먼저 자동화된 테스트 코드를 작성한 후 테스트를 통과하기 위한 코드를 개발하는 방식의 개발 방식을 말한다.

- #### TDD를 이용한 개발방법

  1. 테스트 케이스 작성
  2. 테스트 케이스를 통과하는 코드 작성
  3. 작성한 코드 리팩토링

- #### TDD 장점

  - 소스코드의 품질이 높다.
  - 재설계 및 디버깅 시간이 절감된다.

- #### TDD 단점

  - 단기적 코드일 경우 생산성이 떨어진다.
  - 실제 코드보다 테스트 케이스가 더 커질 수 있다.

- #### 파이썬에서 TDD가 필요한 이유

  - 파이썬에는 정적 타입 검사 기능이 없다. 
  - 동적언어이기 때문에 TDD를 하기에 적합하다.
  - 파이썬은 간결성과 단순함으로 생산성이 높은 반면 런타임 오류가 발생할 수도 있다.
  -  파이썬을 신뢰할 수 있는 유일한 방법은 테스트를 하는 것이다.

- #### 파이썬 테스트 모듈 unittest

  -  unittest는 이미 내장되어 있어 따로 설치하지 않아도 되는 표준 라이브러리이다.

- #### 사용방법

  1.  import unittest
  2. unittest.TestCase 상속받는 하위 클래스 생성
  3. TestCase.assert 메소드를 사용하여 테스트 코드를 간략화
  4. unittest.main() 실행

- #### unittest 

  ```python
  # 테스트할 함수(lib_calc.py)
  
  def add(a, b):
      return a + b
  
  def substract(a, b):
      return a - b
  
  def division(a, b):
      return a / b
  
  def multiply(a, b):
      return a * b
  ```

  ```python
  # 결과값에 대한 테스트 케이스 작성
  
  import unittest
  
  class TddTest(unittest.TestCase):
  
      def testAdd(self):
          result = lib_calc.add(10, 20)
          if result == 30:
              print('testAdd OK')
  
      def testSubstract(self):
          result = lib_calc.substract(20, 30)
  
          if result > 0:
              boolval = True
          else:
              boolval = False
  
          if boolval == False:
              print('testSubstract Error')
  
      def testDivision(self):
          try:
              lib_calc.division(4, 0)
          except Exception as e:
              print(e)
  
      def testMultiply(self):
          result = lib_calc.multiply(10, 9)
  
          if result < 100:
              print('testMultiply Error')
  
  if __name__ == '__main__':
      unittest.main()
  ```

- #### **TestCase.assert 메소드**

  - assertEqual(A, B, Msg) - A, B가 같은지 테스트
  - assertNotEqual(A, B, Msg) - A, B가 다른지 테스트
  -  assertTrue(A, Msg) - A가 True인지 테스트

  - assertFalse(A, Msg) - A가 False인지 테스트
  - assertIs(A, B, Msg) - A, B가 동일한 객체인지 테스트
  - assertIsNot(A, B, Msg) - A, B가 동일하지 않는 객체인지 테스트
  - assertIsNone(A, Msg) - A가 None인지 테스트
  - assertIsNotNone(A, Msg) - A가 Not None인지 테스트
  - assertRaises(ZeroDivisionError, myCalc.add, 4, 0) - 특정 에러 확인

