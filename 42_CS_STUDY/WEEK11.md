# 스트래티지 패턴(Strategy pattern

행위를 클래스로 캡슐화해 동적으로 자유롭게 바꿀 수 있게 해주는 패턴
즉, 전략을 쉽게 바꿀 수 있도록 해주는 디자인 패턴.
게임 프로그래밍에서 게임 캐릭터가 자신이 처한 상황에 따라 공격이나 행동하는 방식을 바꾸고 싶을 때 스트래티지 패턴이 매우 유용함


## 일반 객체지향 기법으로 구현했을 때 발생가능한 문제

- 요구사항
    - 모든 오리는 꽥꽥 소리르 낼 수 있고, 헤엄칠 수 있다.
    - 오리는 모양새가 다르다.
- 결과
    공통사항을 하나로 묶은 Duck 추상 클래스 생성
    - quack: 우는 소리를 내는 기능
    - swim: 수영하는 기능
    - display: 인터페이스(오리는 모양이 다르기 때문에 하위 클래스에서 구현)
    Duck 클래스를 상속받아 다양한 오리 클래스 생성
    - 청둥오리
    - 미국흰죽지
    - 고무오리

```java
public abstract class Duck {
    public void quack() {
        System.out.println("꽥꽥");
    }
    public void swim() {
        System.out.println("헤엄");
    }
    abstract void display();
}
```
```java
public class MallardDuck extends Duck{
    @Override
    void display() {
        System.out.println("천둥오리");
    }
}
```
```java
public class ReadheadDuck extends Duck {
    @Override
    void display() {
        System.out.println("미국흰죽지");
    }
}
```

하지만 이렇게 상속을 통해 구현했을 때 요구사항이 변경됐을 경우?
- 오리에 fly기능을 추가시켜주세요.

```java
public abstract class Duck {
    public void quack() {
        System.out.println("꽥꽥");
    }
    public void swim() {
        System.out.println("헤엄");
    }
    public void fly() {
        System.out.println("훨훨");
    }
    abstract void display();
}
```
그런데 이렇게 해버리면 날 수 없는 오리들에게도 모두 fly기능이 추가 되기 때문에 프로그램에 버그가 생기게 된다.


[스트래티지 패턴](https://2dongdong.tistory.com/43)