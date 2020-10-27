# RxSwift-Intro
> Reactive X is a standerd based on Reactive Programming Prenciples, which exists in sevral languages and platforms. And for that reason Rx skills are considered portable.
> RxSwift is a syncrouns programming library that is based on using observables. 
> Observables are squances of data or events that you can react to, such as data comming back from a web service or events like tabs by users.
> Everything in RxSwift is either an observable sequance or something that reacts to an observable sequance Aka: Observers.
> **The base tybe in RxSwift is Observables**

1. Observables are typed elements that can emit zero or more elements over time to subscribers.
2. Observables will not emit anything untill they have atleast one subsriber.
3. Observables are typed, *Observable<Int>*, so they emit only thier type i.e Int.
4. Everytime on observable emits an event, sunscribers will be able to react to that event.
5. An observable can emit nex events containing elements and when it's done it emits a completed event, whice is the normal termination.
6. If someting goes wrong, an observable will emit an error event, which is considered termination.
  
#### Lifecycle of an observable
- Next Events "Containts elemnts (Ints, Strings, Taps, etc..)"
- Error Event "Observable is terminated, will not emit any more events"
- Completed Event "Observable is terminated, will not emit any more events"

#### Marble Diagrams
Marble Diragrams are data or events that occure over time. 

## Creating Observables 

```swift
let episode: Observable<String> = Observable<String>.just("Episode1")
```
**just: creates an observable sequance with just one element**
- Rx methods are refered to as operators.


```swift
let originalTrilogy = Observable.of("Ep1", "Ep2", "Ep3")
```
**of: takes one or more values of the same type**
- The complier will infer the type as observable of strings.

```swift 
let sequal = Observable.from(["Ep4, "Ep5"])
```
**from: takes an array of values and create an observable of the type of the array**

```swift
let observable = Observable<void>.empty()
```

**empty: creates an empty observable that only emits completed event**

```swift
let observable = Observable<Any>.never()
```

**never: creates observable that doesn't emit anything**

## Subscribing to Observables

```swift
let observable = Observable.of("val1", "val2", "val3")
observable.sunscribe {event in 
print(event.element)
}
```

- Subscribe takes a closure parameter that receives each element emited.
- Each element is wrapped in the next event enum.

```swift
observable.subscribe(onNext: { element in 
print(element)
})
```

*Rx Swift has a **Dispose bag** we add subscribtions to a dispose bag and when its owner is about to be deallocated, it calls the dispose() on the subscribtions.*

```swift
let disposeBag = DisposeBag()
observable.of("val1", "val2")
.subscribe {
print($0)
}.disposed(by: disposeBag)
```
