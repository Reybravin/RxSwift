# RxSwift
RxSwift basics

```swift
enum Event<Element>  {
    case next(Element)      // next element of a sequence
    case error(Swift.Error) // sequence failed with error
    case completed          // sequence terminated successfully
}
```
====
```swift
API.download(file: "http://www...")
	.subscribe(onNext: { data in 
	… append data to temp file
	},
	onError: { error in
	… display error to user
	}, 
	On Completed: {
	… use downloaded file
	})
```
```swift
UIDevice.rx.orientation
	.subscribe(oNext: {current in 
	Switch current:
		case .landscape:
			… re-arrange UI for landscape
		case .portrait: 
			… re-arrange UI for portrait
	}
})
```
```swift
UIDevice.rx.orientation 
	.filter { value in
		return value != . landscape
	}
	.map { _ in 
		return "Portrait is the best!"
	}
	.subscribe(onNext : { string in
		showAlert(text: string)
	})
```

## Schedulers

Equivalent of dispatch queues. 
SerialDispatchQueueScheduler
ConcurrentDispatchQueueScheduler
OperationQueueScheduler

## Creating observables

```swift
Example(of: "just", "of", "them") {
let one = 1
let two = 2
let three = 3
let observable = Observable<Int> = Observable<Int>.just(one)
}
```
