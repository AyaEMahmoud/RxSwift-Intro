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




