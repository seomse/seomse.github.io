---
title: Java Serialization
author: wjrmffldrhrl
date: 2021-01-22 11:30:00 +0800
categories: [java]
tags: [java,wjrmffldrhrl]
---  

# What is Serialize?
- 객체 또는 데이터를 바이트 형태로 변환하는 기술
- 바이트로 변환된 데이터를 다시 객체로 변환하는 기술

이 두가지를 아울러서 이야기한다.

# How to use

기본 타입 맴버와 `java.io.Serializable`인터페이스를 상속받은 객체는 직렬화 할 수 있는 기본 조건을 가진다.

```java
public class User implements Serializable {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return String.format("User{name='%s', age='%s'}", name, age);
    }
}
```

## Serialize

`java.io.ObjectOutputStream`객체 사용

```java
User user = new User("조승현", 25);

try (ByteArrayOutputStream baos = new ByteArrayOutputStream()) {
    try (ObjectOutputStream oos = new ObjectOutputStream(baos)) {
        oos.writeObject(user);

        byte[] serializedUser = baos.toByteArray();
        System.out.println(Base64.getEncoder().encodeToString(serializedUser));

    } catch (IOException e) {
        e.printStackTrace();
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

- base64: 8비트 이진 데이터를 문자코드에 영향을 받지 않는 공통 ASCII 영역의 문자들로만 이루어진 일련의 문자열로 바꾸는 인코딩 방식

### 출력 결과

`rO0ABXNyAA90ZXN0LnRlc3QzLlVzZXICOI3JIFoZcgIAAkkAA2FnZUwABG5hbWV0ABJMamF2YS9sYW5nL1N0cmluZzt4cAAAABl0AAnsobDsirntmIQ=`

## Deserialization

```java
String base64User = Base64.getEncoder().encodeToString(serializedUser);
byte[] serializedUser = Base64.getDecoder().decode(base64User);
try (ByteArrayInputStream bais = new ByteArrayInputStream(serializedUser)) {
    try (ObjectInputStream ois = new ObjectInputStream(bais)) {
        // 역직렬화된 User 객체를 읽어온다.
        Object objectUser = ois.readObject();
        User user = (User) objectUser;
        System.out.println(user.toString());
    }
} catch (IOException | ClassNotFoundException e) {
    e.printStackTrace();
}
```

### 출력 결과

`User{name='조승현', age='25'}`

# Reference

[자바 직렬화, 그것이 알고싶다. 훑어보기편 - 우아한형제들 기술 블로그](https://woowabros.github.io/experience/2017/10/17/java-serialize.html)

[Basics: 직렬화(Serialization)란? (feat. Java)](https://medium.com/@lunay0ung/basics-%EC%A7%81%EB%A0%AC%ED%99%94-serialization-%EB%9E%80-feat-java-2f3eb11e9a8)

[Java Serialization](https://wjrmffldrhrl.github.io/Java-Serialization/)
