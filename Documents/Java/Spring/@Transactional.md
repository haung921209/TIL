# `@Transactional`

일반적으로 DB데이터를 등록/수정/삭제 하는 Service메소드는 @Transactional을 필수적으로 가져갑니다.

->해당 어노테이션(@Transactional)은 메소드내에 Exception이 발생하면 해당 메소드에서 이루어진 모든 DB작업을 초기화 한다.**(모든 처리가 정상적으로 됐을때만 커밋을 진행)**(All or Nothing)



