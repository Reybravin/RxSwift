# RxSwift basics

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
     switch current:
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
   
   let observable1 = Observable<Int> = Observable<Int>.just(one)
   let observable2 = Observable.of(one, two, three)
   let observable3 = Observable.of([one, two, three])
   
   //from operator. This operator creates an observable of individual type instance from a regular array of elements. Only takes an array
   let observable4 = Observable.from([one, two, three])
   
   observable1
     .subscribe(
   	onNext: { element in
	  print(element)
     },
     	onCompleted: {
	  print("Completed")
	}
   )
}
```
### .empty operator

### .never operator

## Disposing and terminating

subscription.dispose()
let disposeBag = DisposeBag()

### .create operator
Defines all the events that will be emitted to subscrbers.

example(of: "DisposeBag") {
  let disposeBag = DisposeBag()
  Observable.of("a", "b", "c")
    .subscribe {
    print($0)
    }
    .disosed(by: disposeBag)
}

example(of: "create"){
  let disposeBag = DisposeBag()
  Observable<String>.create { observe in
    observe.onNext("1")
    observer.onCompleted()
    observer.onNext("?")
    return Disposables.create()
  }
}


