## Operator
- ReactiveX(RxSwift를 만든 곳)에서는 다양한 연산자들을 제공한다.

### Observable 생성 연산자
- Observable을 생성할 수 있는 연산자
- 종류
    - Create
        - 함수를 사용하여 처음부터 Observable을 생성하는 것
        - onNext, onError, onCompleted 메서드를 적절하게 호출하여 Observable로 동작할 수 있도록 함수를 작성해야 한다.
        - 사용법
            ```Swift
                // Observable<Int> 변수를 선언하고 그 변수를 구독
                // 출력값: 10, 20, completed
                let observe = Observable<Int>.create { observer -> Disposable in
                    observer.on(.next(10))
                    observer.onNext(20)
                    observer.onCompleted()
                    return Disposables.create()
                }
                
                observe
                    .subscribe { value in
                        print(value)
                    } onError: { error in
                        print("error")
                    } onCompleted: {
                        print("completed")
                    }
                    .disposed(by: disposeBag)
            ```
    - Just
        - 객체 하나 또는 객체를 하나의 Observabel 이벤트로 변환한다.
        - Just에 null을 넣어도 하나의 이벤트로 방출한다(유의!)
        - 사용법
            ```Swift
                // 하나의 이벤트를 방출
                Observable.just("hello")
                    .subscribe(onNext: { print($0) })
                    .disposed(by: disposeBag)
                // 여러가지 이벤트를 방출하더라도 하나로 방출됨
                Observable.just([1, 2, 3, 4])
                    .subscribe(onNext: { print($0) })
                    .disposed(by: disposeBag)
            ```
    - Of
        - 두개 이상의 값을 넘길때 사용
        - Of의 경우 Observable 배열을 생성해서 이벤트로 변환한다.(From과 차이)
        - 사용법
            ```Swift
                // Observable<[Int]>로 방출
                Observable.of(1, 2, 3, 4, 5)
                    .subscribe(onNext: { print($0) })
                    .disposed(by: disposeBag)
            ```
    - From
        - 배열의 값을 각각 다르게 전달할 때 쓰이는 연산자
        - From의 경우 배열의 각각 원소들을 Observable로 변환한다.(Of와 차이)
        - 사용법
            ```Swift
                // 각 배열의 값을 Observable<Int>로 방출
                Observable.From([1, 2, 3, 4, 5])
                    .subscribe(onNext: { print($0) })
                    .disposed(by: disposeBag)
            ```