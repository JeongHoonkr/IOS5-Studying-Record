## CardGame Step2



##### 핵심리뷰

- 상위모듈(ex : 호스트코드)과 하위모듈(각 객체나 함수)에서 할일을 구분하는 것이 중요

  * 하위 모듈은 판단하는 로직을 최소화하고, 정확한 동작만 해서 상위모듈로 전달
  * 판단은 상위모듈이 하면서, 판단에 따른 액션을 하게 하는것이 가장 좋다.

  ​

##### 생각했던점

> - shuffle 함수를 결국 스스로 짜지 못하고, 서핑을 통해 찾은 함수를 약간 바꿔서 썼다.
>
>   * 조금씩이라도 시작해야 겠다.
>
> - 카드덱이 2배씩 생성되는 문제가 있었는데, 카드덱 객체 생성시 52장을 만들어놓고,
>
>   카드덱을 초기화할때 기존 카드덱에 그대로 append를 해서 2배가됐다.
>
>   결국 문제해결 능력의 부족이 아닐까 생각한다.
>
> - 위와 맞물려서 리팩토링할때 방향에 대한 생각도 아직 매끄럽게 하지 못하고 있다.
>
>   * 이를 해결하기 위해 스택오버플로우에서 여러 코드를 찾아보고 연습하기로 했다.



##### 개선한 문제점들

* **배열, 딕셔너리 확장과 mutating**

> * 기존의 카드덱을 shuffle함수를 통해 섞은 후 새로운 함수를 반환시킬때 mutating을 사용했다.
>
>   왜냐면 기존카드덱을 변경해서 변경된 배열을 리턴시키려는 생각이었기 때문이다.
>
> * 그런데 이 방식은 멀티쓰레드 환경에서 안전하지 않은 단점이 있다고 한다.
>
> * 그래서 이렇게 배열이나 딕셔너리를 확장할때는 기존 값은 그대로 두고, 변경된 값을 리턴하도록
>
>   확장하는 것이 좋다고 한다.
>
>   ​
>
> * 아래처럼 변경하면서 리턴타입도 **Array -> Array<card>**로 변경했다. 모든 어레이에 적용되는 것이 아니기 때문!

```swift
// 기존 코드
extension Array {
    mutating func shuffle() -> Array{
        self.sort { _,_ in arc4random_uniform(2) == 1 }
        return self
    }
}

// 변경코드
extension Array {
    func shuffle() -> Array<Card> {
        return self.sorted { _,_ in arc4random_uniform(2) == 1 } as! Array<Card>
    }
}
```



- **객체 내부를 어떤 의미 단위로 묶을 것인가에 대한 고민**

> - 메인코드에서 모든것을 작성하지 않고 파일(객체)단위로 나누기 시작하면서 항상 어떻게 나누고 묶을 것인가는
>
>   고민해왔던것 같다.
>
> - 카드에 한정지어보면 (인풋, 아웃풋등 제외) 첫설계는 아래와 같다.
>
>   * Card : Card객체 생성
>   * CardSet : 카드 모양및 숫자정보 및 관련 로직
>
> - 그리고 카드덱 과제를 시작하면서 유저에게 보여지는 메뉴가 필요해졌기 때문에, CardSet과 메뉴를 합쳐서
>
>   * CardGameInfo (구 CardSet)를 변경 생성하게 됐다.
>
> - 그런데 마스터가 보기에는 메뉴를 제외한 정보는 Card를 위한 정보 즉 Card객체가 포함하고 있어야 하는
>
>   정보였던것 같다.
>
> - 고민이 없었던 것은 아니지만, 아직 충분히 훈련이 덜됐다는 생각이 들었다. 내용의 변경이 있을때마다
>
>   기존에 생성한 객체와의 관계를 좀 더 숙고해봐야겠다는 생각이 들었다.



```swift
// 기존 코드
extension Array {
    mutating func shuffle() -> Array{
        self.sort { _,_ in arc4random_uniform(2) == 1 }
        return self
    }
}

// 변경코드
extension Array {
    func shuffle() -> Array<Card> {
        return self.sorted { _,_ in arc4random_uniform(2) == 1 } as! Array<Card>
    }
}
```