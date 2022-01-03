
### [1교시] 개념잡기 - RxSwift를 사용한 비동기 프로그래밍

1. Observable
- Observable create
- subscribe 로 데이터 사용
- Disposable 로 작업 취소

2. Sugar API
- 간단한 생성 : just, from
- 필터링 : filter, take
- 데이터 변형 : map, flatMap


📌 Async : 비동기 
```swift 
@IBAction func onLoadAsync(_ sender: Any) {
        DispatchQueue.global().async {
            let image = self.loadImage(from: self.IMAGE_URL)

            DispatchQueue.main.async {
                self.imageView.image = image
            }
        }
    }

```
📌 PromiseKit

```swift
func promiseLoadImage(from imageUrl: String) -> Promise<UIImage?> {
        return Promise<UIImage?>() { seal in
            asyncLoadImage(from: imageUrl) { image in
                seal.fulfill(image)
            }
        }
    }
```

📌 RxSwift 
- Async 한 작업을 간단하게 하기 위한 유틸리티 
```swift
func rxswiftLoadImage(from imageUrl: String) -> Observable<UIImage?> {
        return Observable.create { seal in
            asyncLoadImage(from: imageUrl) { image in
                seal.onNext(image)
                seal.onCompleted()
            }
            return Disposables.create()
        }
    }
```

