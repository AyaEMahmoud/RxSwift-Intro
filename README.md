# RxSwift-Intro
> Reactive X is a standard based on Reactive Programming Principles, which exists in several languages and platforms. And for that reason Rx skills are considered portable.
> RxSwift is a synchronous programming library that is based on using observables. 
> Observables are sequences of data or events that you can react to, such as data coming back from a web service or events like tabs by users.
> Everything in RxSwift is either an observable sequence or something that reacts to an observable sequence Aka: Observers.
> **The base type in RxSwift is Observables**

1. Observables are typed elements that can emit zero or more elements over time to subscribers.
2. Observables will not emit anything until they have at least one subscriber.
3. Observables are typed, *Observable<Int>*, so they emit only their type i.e Int.
4. Every time on observable emits an event, subscribers will be able to react to that event.
5. An observable can emit next events containing elements and when it's done it emits a completed event, which is the normal termination.
6. If something goes wrong, an observable will emit an error event, which is considered termination.
  
#### Lifecycle of an observable
- Next Events "Contains elements (Ints, Strings, Taps, etc..)"
- Error Event "Observable is terminated, will not emit any more events"
- Completed Event "Observable is terminated, will not emit any more events"

#### Marble Diagrams
Marble Diagrams are data or events that occur over time. 

## Creating Observables 

```swift
let episode: Observable<String> = Observable<String>.just("Episode1")
```
**just: creates an observable sequence with just one element**
- Rx methods are referred to as operators.


```swift
let originalTrilogy = Observable.of("Ep1", "Ep2", "Ep3")
```
**of: takes one or more values of the same type**
- The complier will infer the type as observable of strings.

```swift 
let sequel = Observable.from(["Ep4, "Ep5"])
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
observable.subscribe {event in 
print(event.element)
}
```

- Subscribe takes a closure parameter that receives each element emitted.
- Each element is wrapped in the next event enum.

```swift
observable.subscribe(onNext: { element in 
print(element)
})
```

*Rx Swift has a **Dispose bag** we add subscriptions to a dispose bag and when its owner is about to be deallocated, it calls the dispose() on the subscriptions.*

```swift
let disposeBag = DisposeBag()
observable.of("val1", "val2")
.subscribe {
print($0)
}.disposed(by: disposeBag)
```

### Traits
- Single: will emit a single next event or an error event.
- Completable: will emit completed event, or error event, but will not emit any next events.
- Maybe: emits one event only, next, or maybe, or error.

### Do Operator and Side Effects

do inserts side effects that will handle behaviours without changing the emitted event.

```swift
Observer.of("val1", "val2")
.do(onNext: {element in 
print($0) 
}, onComplete: {element in 
print($0)
},onSubscribe: {element in 
print($0)
}, onSubscribed: {element in 
print($0)
}, onDispose: {element in 
print($0)
})
```

# Subjects
> Comprise of two parts
> - Observable "Can be subscribed to"
> - Observer "Can receive new events"

*This allows the observables with non finite sequences to add new elements and then emit them to subscribers*

## Subject Types
- Publish Subject
- Behaviour Subject
- Reply Subject
- Variable
