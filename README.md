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
  - assertTrue(A, Msg) - A가 True인지 테스트
- assertFalse(A, Msg) - A가 False인지 테스트
  - assertIs(A, B, Msg) - A, B가 동일한 객체인지 테스트
  - assertIsNot(A, B, Msg) - A, B가 동일하지 않는 객체인지 테스트
  - assertIsNone(A, Msg) - A가 None인지 테스트
  - assertIsNotNone(A, Msg) - A가 Not None인지 테스트
  - assertRaises(ZeroDivisionError, myCalc.add, 4, 0) - 특정 에러 확인
  
- **TestCase.assert 메소드 사용**

```python
# TestCase.assert 메소드를 사용하여 에러를 발생

import unittest

class TddTest(unittest.TestCase):

    def testAdd(self):
        result = lib_calc.add(10, 20)

        # 결과 값이 일치 여부 확인
        self.assertEqual(result, 31)

    def testSubstract(self):
        result = lib_calc.substract(20, 10)

        if result > 10:
            boolval = True
        else:
            boolval = False

        # 결과 값이 True 여부 확인
        self.assertTrue(boolval)

    def testDivision(self):
        # 결과 값이 ZeroDivisionError 예외 발생 여부 확인
        self.assertRaises(ZeroDivisionError, lib_calc.division, 4, 1)

    def testMultiply(self):
        nonechk = True

        result = lib_calc.multiply(10, 9)

        if result > 100:
            nonechk = None

        # 결과 값이 None 여부 확인
        self.assertIsNone(nonechk)

if __name__ == '__main__':
    unittest.main()

# 결과
# 1) 테스트가 실패해도 다른 테스트에 영향을 미치지 않음
# 2) 실패한 위치와 이유를 알 수 있음
```

- **TestCase 메소드**
  - setUp() 메소드로 전역 변수에 값을 지정
  - tearDown() 메소드로 “ 결과 값 : ” 텍스트 출력

```python
import unittest

class TddTest(unittest.TestCase):

    aa = 0
    bb = 0
    result = 0

    # 매 테스트 메소드 실행 전 동작
    def setUp(self):
        self.aa = 10
        self.bb = 20

    def testAdd(self):
        self.result = lib_calc.add(self.aa, self.bb)

        # 결과 값이 일치 여부 확인
        self.assertEqual(self.result, 31)

    def testSubstract(self):
        self.result = lib_calc.substract(self.aa, self.bb)

        if self.result > 10:
            boolval = True
        else:
            boolval = False

        # 결과 값이 True 여부 확인
        self.assertTrue(boolval)

    def testDivision(self):
        # 결과 값이 ZeroDivisionError 예외 발생 여부 확인
        self.assertRaises(ZeroDivisionError, lib_calc.division, 4, 1)

    def testMultiply(self):
        nonechk = True

        self.result = lib_calc.multiply(10, 9)

        if self.result > 100:
            nonechk = None

        # 결과 값이 None 여부 확인
        self.assertIsNone(nonechk)

    # 매 테스트 메소드 실행 후 동작
    def tearDown(self):
        print(' 결과 값 : ' + str(self.result))

if __name__ == '__main__':
    unittest.main()
    
# 결과
# setUp() 메소드로 지정한 값으로 테스트를 수행
# tearDown() 메소드로 각각의 테스트 메소드 마다 “ 결과 값 : ” 텍스트 출력
```

- **실행 명령어**
  - python -m unittest discover [option]
    1. -v : 상세 결과
    2. -f : 첫 번째 실패 또는 오류시 중단
    3. -s : 시작할 디렉토리
    4. -p : 테스트 파일과 일치하는 패턴
    5.  -t : 프로젝트의 최상위 디렉토리

- 참고자료
  - https://www.slideshare.net/hosunglee948/python-52222334
  - https://www.slideshare.net/ssuser163469/tdd-101