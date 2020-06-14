# @ConfigurationProperties

1. prefix = "text"
- text의 이름을 가진 Configuration을 찾아 주입시킨다.
- @Component 등의 bean 등록 어노테이션을 사용할 때 사용함.
- prefix나 value 모두로 사용할 수 있음.

2. ignoreInvalidFields
- default는 false

3. ignoreUnknownFields
- default는 true