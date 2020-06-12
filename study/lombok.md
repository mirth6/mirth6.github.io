## lombok

getter, setter를 어노테이션으로 자동 생성해주는 자바 라이브러리

```
@Getter
@Setter
@slf4j로깅
```



#### 동작원리

Annotation Processing

- 컴파일 타임에 처리과정 중 Annotation Processing과정이 있는데 등록된 lombokprocessor가 Annotation을 참조하여 그에 맞는 코드를 자동으로 bytecode(class)에 추가

Instrumentation

- Loadtime 또는 Runtime에 bytecode(class)에 대해 직접 수정을 가해서, 소스 파일의 수정 없이 원하는 기증을 부여하는 기법

- eclipse.ini

  ```
  -javaagent:C:\dev\eclipse\lombok.jar
  ```

- Instrumentation의 사용 예로 모니터링 대상이 되는 어플리케이션의 수정 없이 성능 측정에 필요한 요소들을 삽입할 수 있다. AOP를 구현하는 핵심기술

  

#### 주의점

https://kwonnam.pe.kr/wiki/java/lombok/pitfall



#### 설치

https://duzi077.tistory.com/142