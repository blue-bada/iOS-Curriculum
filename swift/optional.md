# Optional

Optional\(이하 옵셔널\)은 값이 있을수도, 없을수도 있는 변수에서 쓰이는 문법이며, Swift의 특징이자 장점이라고 할 수 있습니다.

개발을 할 때 null\(이하 nil\)값은 주요 버그의 원인이 되는 경우가 많습니다. 그래서 최근 Kotlin의 Nullable, Java의 옵셔널처럼 해당 값이 null이 들어갈 수 있는 경우에 옵셔널을 이용하여 null에 의한 버그를 방지하는 경우가 많습니다.

Swift는 거기에 좀 더 엄격하게 관리합니다. 다른 언어는 해당 문법 없이 Integer에도 nil을 넣을 수 있지만, Swift는 **기본적으로** 변수에 nil값이 **절대로** 들어갈 수 없습니다. 만약 Int값에 nil이 들어갈 가능성이라도 있다면 

```bash
Nil cannot be assigned to type 'Int'
```

라는 오류를 띄우면서 막습니다. 그래서 만에 하나라도 nil값이 들어가는 변수라면, 옵셔널을 사용해야합니다.

그러면 옵셔널을 사용하려면 어떻게 해야될까요? 다음과 같이 해주시면 됩니다.

```swift
var num : Int?
num = nil
```

이렇게 하면 옵셔널을 통하여 값 안에 nil을 넣을 수 있게 되었습니다.

옵셔널은 빈 상자와 같다고 볼 수 있습니다. 빈 상자를 꺼내기 전까지는 안에 Integer값이 있을수도 있고 없을수도 있는겁니다. Optional\(Int\)같은 느낌이라고 보시면 됩니다.

그러면 옵셔널에서 Int값을 꺼내 사용하려면, 상자를 열어야할겁니다. 옵셔널에서 상자를 꺼내는 방법은 2가지가 있습니다. 강제로 여는 방법과, 하나씩 값을 체크하는 방법이 있습니다.

1. 강제로 여는 방법\(강제 언래핑\)

강제 언래핑은 강제로 상자를 여는 방법입니다. Optional\(Int\)라면 Int로 바뀌게 됩니다. 방법은 다음과 같습니다.

```swift
var num :Int? = 30
var value : Int = num!
```

느낌표 하나만 넣어주면, 간단하게 바뀌게 됩니다.

강제 언래핑을 이용하면 옵셔널을 쉽게 벗길 수 있지만, 강제로 하는만큼 문법상으로 위험합니다. 이유는 다음과 같습니다.

```swift
import Foundation

var num :Int? = nil
var value : Int = num!
print(value)
```

이렇게 nil을 넣고 한번 실행해보겠습니다.

```bash
Fatal error: Unexpectedly found nil while unwrapping an Optional value: file MyPlayground.playground, line 4
```

오류 뜻은 "옵셔널을 언래핑하면서 예상치못한 nil을 찾았습니다", 흔히 얘기하는 NullPointException이 걸렸습니다. 저런 오류가 생기면 개발할 때 또다른 버그를 일으키는 원인이 됩니다.  그래서 이런 점을 미연에 방지하기 위해서 강제 언래핑은 비추천합니다. 굳이 쓴다면 어떤일이 있어도 nil이 안 나오는 경우에만 사용하시기 바랍니다.

2. 값 체크해보기\(옵셔널 바인딩\)

옵셔널 바인딩은 이 값이 nil인지 아닌지 한번 확인하는 과정으로, nil인경우와 nil이 아닌 경우에 따라 행동을 다르게 해주는 방식입니다. 방식은 다음과 같습니다.

```swift
func printName(name : String){
    print(name)
}

 var myName: String? = nil

 if let name = myName {
     printName(name: name)
 }
```

이렇게 실행하게 되면 아무 일도 일어나지 않게 됩니다. 값이 nil이기때문에 if에서 false가 나와 동작하지 않습니다. 만약 값이 있으면, printName이 동작하게 되면서 출력됩니다. if let은 값이 바인딩될 때만 true로 동작하게 됩니다. 그래서 옵셔널 바인딩이라 합니다.

옵셔널 바인딩은 옵셔널의 값을 꺼낼 때 대표적으로 쓰이는 방법으로, 가장 안전한 방법입니다. 그래서 옵셔널에서 값을 꺼낼 때는 이 방식을 쓰는 것을 추천합니다.

2-1. 연속적으로 열어보면서 nil값이 하나라도 있으면 nil을 반환\(옵셔널 체이닝\)

이 방법은 옵셔널 바인딩과 비슷한데, 하위 property가 있을 때 사용되는 방식입니다. 주로 class나 struct에 많이 사용됩니다. 예시는 다음과 같습니다.

```swift
class Dining {
    var meal: Meal?
}
class Meal {
    var menu: String = "까르보나라돈까스"
}

let haksik = Dining()
// haksik.meal = Meal()

if let haksikMenu = haksik.meal?.menu {
    print("오늘 학식 메뉴 : \(haksikMenu)")
} else {
    print("오늘 학식 메뉴는 없습니다.")
}
```

실행을 하면 결과는 "오늘 학식 메뉴는 없습니다."가 출력됩니다. 왜냐하면 Dining 내부의 meal이 nil인 상태라서 그렇습니다. 만약 오늘의 학식 메뉴를 보고 싶으면 9번 줄을 추가해주면 됩니다. 그러면 Dining 내부의 meal 값이 nil이 아니게 되면서 meal 내부의 menu까지 가게 되고, menu에 값이 있기 때문에 오늘 학식 메뉴가 나오게 됩니다.

여기서 11번 줄의 haksik.meal?.menu에서 meal?은 nil이 될수도 있고, 아닐수도 있기 때문에 ?표시를 붙여 옵셔널이라고 표시해집니다.

이처럼 체인처 하위 프로퍼티로 가면서 하나라도 nil이 나올 경우 nil을 반환하는 방식을 옵셔널 체이닝이라고 합니다.

이러한 옵셔널은 서버에서 정보를 받을 때 많이 사용됩니다. 서버에 있는 정보는 값이 있을수도, 없을수도 있어서 옵셔널이 많은 도움이 됩니다. 위에서 예시로 준 학식만 해도 학식이 있는 경우도, 없는 경우도 있어서 실제로 옵셔널로 저장해야 합니다.

이렇듯 옵셔널은 개발할 때 많은 도움을 주는 문법이며, 잘 활용하려면 옵셔널에 대해 배워보는 게 좋을겁니다!

