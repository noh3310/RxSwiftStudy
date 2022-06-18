## Observable
- 값이 변경된 것을 내보낸다.
- Observable은 세가지 타입의 이벤트를 방출할 수 있다. 
    - onNext: Observable의 값이 변경되었을 때 Next 이벤트 전달
    - onError: 에러 발생시 Error 이벤트 전달
    - onCompleted: 오류가 발생하지 않고, 마지막 onNext가 호출된 후 이 Completed 이벤트 전달

### Hot & Cold Observable
- Hot Observable
    - 값이 변경되었을 때 구독한것과 관계없이 바로 이벤트를 방출한다.
    - 나중에 구독한 Observer의 경우 중간부터 이벤트를 알림받을 수 있다.
- Cold Observable
    - Observer가 subscribe하기를 기다렸다가 구독 하자마자 변경된 값을 전체다 전달하는 것

## Observer
- Observable을 구독하고, 구독한 Observable의 값 변경을 알림받는다.
    - Observer가 Observable을 구독하는것을 subscribe라고 한다.
- 여러개의 Observer가 하나의 Observable을 구독할 수 있다.

## DisposeBag
- Observable은 Error나 Completed 이벤트가 방출되거나, ```dispose()```를 호출하면 종료된다.
- DisposeBag은 ARC와 메모리관리를 위해 RxSwift에서 추가된 개념이다. 
- 부모 오브젝트가 메모리에서 해제되면, DisposeBag에서 Observable 오브젝트가 삭제된다.
    - DisposeBag을 보유하고 있는 인스턴스에서 ```deinit()```이 호출되면 Observer은 Observable을 자동으로 구독 해제한다.
    - DisposeBag을 사용하면 ARC는 평소와 같이 메모리를 회수할 수 있다.
