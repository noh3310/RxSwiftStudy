# Single
- Observable의 경우 onNext, onError, onCompleted 세가지 이벤트를 방출할 수 있지만 Single은 onCompleted, onError를 방출할 수 있다.
- Single은 한번만 방출할 수 있고, 한번 방출했다면 Dispose된다.
- 사용법
    ```Swift
    enum MyError: Error {
        case fail
    }
    
    // success, failure 이벤트만 방출 가능
    // single 변수는 3가지 이벤트를 방출하지만 single은 하나만 방출할 수 있기 때문에 .success(1)만 방출되고 dispose됨
    let single = Single<Int>.create { single in
        single(.success(1))
        single(.success(2))
        single(.failure(MyError.fail))
        return Disposables.create()
    }
    
    // 출력값: 1, disposed
    single
        .subscribe { value in
            print(value)
        } onFailure: { error in
            print(error.localizedDescription)
        } onDisposed: {
            print("disposed")
        }
        .disposed(by: disposeBag)
    ```