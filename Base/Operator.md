## Operator
- ReactiveX(RxSwift를 만든 곳)에서는 다양한 연산자들을 제공한다.

### Observable 생성 연산자
- Observable을 생성할 수 있는 연산자
- 예제
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
        - 두개 이상의 값을 넘길 때 사용
        - From의 경우 배열의 각각 원소들을 Observable로 변환한다.(Of와 차이)
        - 사용법
            ```Swift
                // 각 배열의 값을 Observable<Int>로 방출
                Observable.From(1, 2, 3, 4, 5)
                    .subscribe(onNext: { print($0) })
                    .disposed(by: disposeBag)
            ```