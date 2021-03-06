## Function Basic



#### 1. 함수 기본 사용 

```swift
// 매개변수와 반환값이 없는 함수
func making () { print ("의미없다") }
making()

// 사람이름을 매개변수로 받아 인사하는 내용을 출력하는 함수
func sayHello (to name: String) { print ("Hello, \(name)") }
sayHello(to: "정훈")   // Hello, 정훈

// 더하기의 결과값을 출력하는 함수
func plusNum (numA: Int, numB: Int) { print(numA + numB) }
plusNum(numA: 5, numB: 7) // 12

// 더하기의 결과값을 반환하는 함수
func plusNumReturn (numA: Int, numB: Int) -> Int { return (numA + numB) }
print(plusNumReturn(numA: 5, numB: 7))
```



#### 2. 반환값이 여러개인 함수

> 사용문법 : Switch, Tuple
>
> 반환값이 여러개일 경우 튜플을 활용하면 된다. 이 경우 튜플의 인덱스를 사용하여 접근해도 되지만
>
> 아래와 같이 반환값의 이름을 붙여주는 것이 더 가독성이 좋다.

```swift
func pointToGrade (from score: Int) -> (point: Double, grade: String)
{
    switch score {
    case 96...100 :
        return (4.5, "A+")
    case 91...95 :
        return (4.0, "A")
    case 81...90 :
        return (3.5, "B+")
    case 70...80 :
        return (3.0, "B")
    default:
        return (2.5, "C")
    }
}
// 함수를 호출하여 상수에 담기
let myGrade = pointToGrade(from: 85)

// 튜플형태의 반환값에 이름을 붙여, 그 이름에 접근하여 사용하기
print("평점은 \(myGrade.point)이고, 등급은 \(myGrade.grade)입니다.")
```



#### 3. 가변 파라미터

> 파라미터에 값을 여러개 받을 수 있음

```swift
func greeting (to names: String...) {
    for name in names {
        print ("어서와 \(name) Xcode는 처음이지?")
    }
}

print(greeting(to: "송", "삼규", "승민", "일한"))

// 점수를 받아서 평균을 반환하기
func getAverageScore (from score: Int...) -> Double {
    var result: Double = 0.0
    for i in score {
        result += Double(i)
    }
    return result/Double(score.count)
}
print(getAverageScore(from: 65,70,80,75,100))

// 생각해볼거리 : UI를 할때 사용해볼 수 있을듯? 
```



#### 4. 파라미터의 기본값

> 파라미터에는 기본값을 줄 수 있다. 즉 파라미터 이름과 타입뿐 아니라 디폴트로 값을 지정해줄 수 있다.
>
> 디폴트 값은 **아래 이미지에서처럼 호출시 그대로 사용할 수도 변경할 수도 있다.** 
>
> ![dd](http://postfiles2.naver.net/MjAxNzEwMDVfMTE2/MDAxNTA3MjA1MzQzMDY2.HR2I2qDRlcS28EZgPTbX0-9BydrpJh1B3piCBvMWinMg.QVvbI68Sw3BaRrf8W6bDPp5sQFKbj3srWjqhLiQAZdkg.PNG.bb_9900/스크린샷_2017-10-05_오후_9.07.31.png?type=w773)
>
> 그대로 사용한다면 기본값 인자가 없는 함수를 사용하면 된다.

```swift
func multiple (firstNum: Int!, secondNum: Int?, punctuation: String = "!") {
    let numFirst: Int = firstNum
    if let numSecond = secondNum {
        print ("\(numFirst) + \(numSecond) = \(numFirst + numSecond) 입니다.\(punctuation)")
    }
}
print(multiple(firstNum: 4, secondNum: 5))
```


