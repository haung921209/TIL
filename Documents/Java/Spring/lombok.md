1. NoArgsConstructor 접근 권한은 최소화 하는 것이 좋다.
   - 따라서, 실무에서는 @NoArgsConstructor(access = AccessLevel.PROTECTED)를 사용하면 객체 생성시 안정성을 어느정도 보장받을 수 있다.
2. 