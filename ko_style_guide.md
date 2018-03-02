# raywenderlich.com 공식 Swift 스타일 가이드  

이 스타일 가이드는 다른 것들과는 다소 차이가 있을 수 있습니다.
왜냐하면, 출판물 및 웹용 가독성을 중점을 두고 있기 때문입니다.
raywenderlich.com에는 많은 저자가 모여 있지만, 책, 튜토리얼, 시작 킷트에서 일관성이 있는 코드를 유지하기 위해 이 스타일 가이드를 작성했습니다.

큰 틀의 지침서를 목표로 간결하고 가독성이 좋고 단순하게 만들기 위함입니다.

Objective-C 코딩 지침서를 여기를 참고하세요。  
[Objective-C 스타일 가이드]（https://github.com/raywenderlich/objective-c-style-guide）  

## Table of Contents

* [Naming](#naming)
  * [Class Prefixes](#class-prefixes)
* [Spacing](#spacing)
* [Comments](#comments)
* [Classes and Structures](#classes-and-structures)
  * [Use of Self](#use-of-self)
* [Function Declarations](#function-declarations)
* [Closures](#closures)
* [Types](#types)
  * [Constants](#constants)
  * [Optionals](#optionals)
  * [Struct Initializers](#struct-initializers)
  * [Type Inference](#type-inference)
  * [Syntactic Sugar](#syntactic-sugar)
* [Control Flow](#control-flow)
* [Semicolons](#semicolons)
* [Language](#language)
* [Smiley Face](#smiley-face)
* [Credits](#credits)


## Naming

메소드 및 변수는 소문자로 시작한다.  
메소드, 변수는 소문자로 시작해야 하지만, 모듈범위의 클래스명과 상수는 대문자로 한다.  

**추천:**

```swift
let MaximumWidgetCount = 100

class WidgetContainer {
  var widgetButton: UIButton
  let widgetHeightPercentage = 0.85
}
```

**비추천:**

```swift
let MAX_WIDGET_COUNT = 100

class app_widgetContainer {
  var wBut: UIButton
  let wHeightPct = 0.85
}
```

문맥이 정확하지 않는 경우, 함수 및 이니셜라이저에서는 전체로 이해할 수 있는 이름으로 구성된 매개변수가 좋습니다.  
외부 매개변수명도 포함됩니다. 그것은 함수호출을 더 쉽게 이해할 수 있습니다.  

```swift
func dateFromString(dateString: NSString) -> NSDate
func convertPointAt(#column: Int, #row: Int) -> CGPoint
func timedAction(#delay: NSTimeInterval, perform action: SKAction) -> SKAction!

// would be called like this:
dateFromString("2014-03-14")
convertPointAt(column: 42, row: 13)
timedAction(delay: 1.0, perform: someOtherAction)
```

메소드의 경우, 메소드명에 첫번째 매개변수의 참조를 포함하거나 표준 애플 기준에 따른다.
애플사 기준
https://developer.apple.com/library/ios/documentation/swift/conceptual/swift_programming_language/Methods.html#//apple_ref/doc/uid/TP40014097-CH15-XID_356*  

```swift
class Guideline {
  func combineWithString(incoming: String, options: Dictionary?) { ... }
  func upvoteBy(amount: Int) { ... }
}
```

튜토리얼, 책, 댓글등의 함수를 참조시, 호출하는 쪽의 관점에서 필수 매개변수명을 포함하고 있어야 합니다.
문맥이 명확하고 정확한 이름이 중요하지 않는 경우, 메소드명만 사용할 수 있습니다.

> Call `convertPointAt(column:row:)` from your own `init` implementation.
>
> If you implement `didSelectRowAtIndexPath`, remember to deselect the row when you're done.
>
> You shouldn't call the data source method `tableView(_:cellForRowAtIndexPath:)` directly.


### Class Prefixes

Swift의 형은 모두 자동으로 모듈단위의 네임스페이스입니다.
따라서 이름때문에 충돌날 수 있는 것을 최소화하기 위해 프리픽스(접두사)는 필요하지 않습니다.
같은 이름으로 다른 모듈의 경우 모듈명과 모델명을 붙여서 명확하게 할 수 있습니다：  


```swift
import MyModule

var myClass = MyModule.MyClass()
```

Swift의 형에는 프리픽스(접두사)를 사용하지 마십시오.  

Objective-C에서 사용하는 Swift를 공개하는 경우 알맞은 프리픽스를 제공할 수 있습니다.  
（아래 [Objective-C 스타일 가이드]처럼（https://github.com/raywenderlich/objective-c-style-guide））：  

```swift
@objc (RWTChicken) class Chicken {
   ...
}
```


## Spacing

탭보다 2칸의 공백 들여쓰기가 공백을 절약하고 줄바꿈은 하지 마십시오.
Xcode에서 이 환경을 설정하세요.
메소드의 괄호 및 기타 괄호( `if`/` else`/ `switch`/` while`등）,  
항상 문장과 같은 줄에 오픈한 새로운 라인을 닫습니다.
　　

**추천:**
```swift
if user.isHappy {
  //Do something
} else {
  //Do something else
}
```

**비추천:**
```swift
if user.isHappy
{
    //Do something
}
else {
    //Do something else
}
```

메소드 사이에 쉽게 확인할 수 있도록 하나의 빈줄이 있어야 합니다.   
하나의 메소드에 공백구분이 너무 많은 경우 몇 가지 메소드로 분할하는 것이 좋습니다.  

## Comments

주석을 필요로 하는 경우에는 코드의 특정 부분이 무엇인지를 설명하는 주석을 사용합니다.
주석관리를 통해 최신 상태로 유지해야 합니다.

코드는 가능한 문서로 있어야 하기에 인라인 블록 주석을 피하십시오.
예외: 문서를 생성하는데 사용하는 주석에는 적용되지 않습니다.    


## Classes and Structures

좋은 클래스 정의의 예를 보여줍니다.  

```swift
class Circle: Shape {
  var x: Int, y: Int
  var radius: Double
  var diameter: Double {
    get {
      return radius * 2
    }
    set {
      radius = newValue / 2
    }
  }

  init(x: Int, y: Int, radius: Double) {
    self.x = x
    self.y = y
    self.radius = radius
  }

  convenience init(x: Int, y: Int, diameter: Double) {
    self.init(x: x, y: y, radius: diameter / 2)
  }

  func describe() -> String {
    return "I am a circle at \(centerString()) with an area of \(computeArea())"
  }

  override func computeArea() -> Double {
    return M_PI * radius * radius
  }

  private func centerString() -> String {
    return "(\(x),\(y))"
  }
}
```

위 예제는 다음 스타일 가이드를 제공하고 있습니다:  

속성, 변수, 상수인수는 형을 지정하고 콜론 앞이 아닌 뒤에 공백을 넣습니다.
예: `x: Int`,  `Circle: Shape`  
공통의 목적/콘텍스트를 공유하는 경우 같은 행에 여러개의 변수와 스트럭쳐를 정의한다.
getter/setter 정의 및 속성도 들여쓰기 합니다.
기본적으로 `internal`등의 한정자를 추가하지 마십시오.
메소드를 재정의하는 경우도 마찬가지로 액세스한정자를 반복하지 않습니다.  

### Use of Self

Swift는 개체의 속성 접근메소드 호출에서 `self`를 필요로 하지 않기 때문에 간결하게 하기 위해 `self` 사용을 피하십시오.  

속성명과 인수의 초기화에서 구별을 위해 필요한 경우 폐쇄에서 속성을 참조하는 경우에는 명확하게 하기 위해 `self`를 사용하십시오.  


```swift
class BoardLocation {
  let row: Int, column: Int

  init(row: Int,column: Int) {
    self.row = row
    self.column = column

    let closure = { () -> () in
      println(self.row)
    }
  }
}
```

## Function Declarations

함수는 짧고 간결하게 여는 괄호를 포함하여 한줄로 요약합니다:  

```swift
func reticulateSplines(spline: [Double]) -> Bool {
  // reticulate code goes here
}
```

긴 이름의 함수는 알맞은 위치에서 줄바꿈을 하고 연속적인 행에 들여쓰기를 추가합니다:  

```swift
func reticulateSplines(spline: [Double], adjustmentFactor: Double,
    translateConstant: Int, comment: String) -> Bool {
  // reticulate code goes here
}
```


## Closures

가능한 TrailingClosures구문을 사용합시다. 모든 경우에 의미를 전달할 수 있는 설명적인 인수명을 사용합시다:
TrailingClosures참고구문:　http://qiita.com/edo_m18/items/1d93af7de75c6d415f19#2-6  

```swift
return SKAction.customActionWithDuration(effect.duration) { node, elapsedTime in
  // more code goes here
}
```

문맥이 명확한 단일형태의 closure는 암시적인 리턴을 사용합시다:

```swift
attendeeList.sort { a, b in
  a > b
}
```


## Types

사용가능한 경우 반드시 Swift의 네이티브형을 사용합시다.
필요에 따라 완전한 세트를 사용할 수 있도록 Swift는. Objective-C를 브릿지해서 사용할 수 있습니다.

**추천:**
```swift
let width = 120.0                                    //Double
let widthString = (width as NSNumber).stringValue    //String
```

**비추천:**
```swift
let width: NSNumber = 120.0                                 //NSNumber
let widthString: NSString = width.stringValue               //NSString
```

SpriteKit 코드로 변환을 피해서 코드가 더 간결해진다면 'CGFloat'를 사용합니다。  

### Constants

상수는 `let`으로 정의합니다. 변수는 `var`로 정의합니다.  
`let`키워드를 사용하여 상수를 알맞게 정의하면 아마도 ‘var’보다 훨씬더 좋은 ‘let’을 사용하는 것입니다.

**Tip:** *이 기준을 충족하는데 도움이 되는 기술로 모든 것을 상수로 정의한 컴파일러에 무리가 되는 것만 변수로 변경하는 것입니다.


### Optionals

값을 허용하는 곳에서는 변수와 함수의 리턴형식을 선택적 ‘?’으로 선언합시다.
나중에 사용하기 전에 초기화하는 것으 확실한 인스턴스 변수에만 Implicitly Unwrapped Optional형’!’으로 선언합시다.
예로 , viewDidLoad초기화하는 subview등이 있습니다.

선택적 값에 접근할 경우 한번 사용하고 있는 값이거나 체인에서 많은 선택사항이 있는경우. Optional chaining을 사용합시다:

```swift
myOptional?.anotherOne?.optionalView?.setNeedsDisplay()
```

1번 실행 및 여러번 실행을 수행하는데 적합한 경우는 optional binding을 사용합시다:  
참고: http://qiita.com/cotrpepe/items/e30c7442733b93adf46a#3-optional-binding  

```swift
if let view = self.optionalView {
  // do many things with view
}
```

### Struct Initializers

레거시 CGGeometry 생성자보다 네이티브 Swift구조체 이니셜라이저를 사용합시다.  

**추천:**
```swift
let bounds = CGRect(x: 40, y: 20, width: 120, height: 80)
var centerPoint = CGPoint(x: 96, y: 42)
```

**비추천:**
```swift
let bounds = CGRectMake(40, 20, 120, 80)
var centerPoint = CGPointMake(96, 42)
```

### Type Inference

Swift 컴파일러는 변수와 상수 타입추론을 할 수 있습니다. 명시적인 형을 지정할 수 있지만 대부분의 경우 필요가 없습니다.
컴팩트한 코드에 컴파일러 상수 또는 변수 형 추론을 이용합시다.

**추천:**
```swift
let message = "Click the button"
var currentBounds = computeViewBounds()
```

**비추천:**
```swift
let message: String = "Click the button"
var currentBounds: CGRect = computeViewBounds()
```

**NOTE**　이 지침을 준수하여 설명하려는 이름을 선택하는 것은 이전보다 더 중요하게 될 것입니다.   

### Syntactic Sugar

제네릭 구문에서는 형 선언의 바로가기를 사용합시다.  

**추천:**
```swift
var deviceModels: [String]
var employees: [Int: String]
var faxNumber: Int?
```

**비추천:**
```swift
var deviceModels: Array<String>
var employees: Dictionary<Int, String>
var faxNumber: Optional<Int>
```



## Control Flow

`for` loop over the `for-condition-increment`보다,`for-in`을 사용합시다.  

**추천:**
```swift
for _ in 0..<3 {
  println("Hello three times")
}

for person in attendeeList {
  // do something
}
```

**비추천:**
```swift
for var i = 0; i < 3; i++ {
  println("Hello three times")
}

for var i = 0; i < attendeeList.count; i++ {
  let person = attendeeList[i]
  // do something
}
```


## Semicolons

코드의 각 문장뒤에 세미콜론이 필요하지 않습니다. 한줄에 여러 문장을 결합하는 경우에만 필요합니다.

세미콜론을 사용하여 여러 줄을 한줄로 사용하지 마십시오.

이 규칙의 유일한 예외는 ‘for-conditional-increment’입니다. 그러나 가능한 ‘for-in’을 사용합니다.  

**추천:**
```swift
var swift = "not a scripting language"
```

**비추천:**
```swift
var swift = "not a scripting language";
```

**NOTE**: Swift는 세미콜론을 생략해도 되는 JavaScript와는 상당히 다릅니다. 세미콜론을 생략하는 것이 일반적으로는 안전하지 않다고 이야기합니다.(http://stackoverflow.com/questions/444080/do-you-recommend-using-semicolons-after-every-statement-in-javascript)



## Language

Apple의 API와 일치시키기 위해 미국식 영어철자를 사용하십시오.

**추천:**
```swift
var color = "red"
```

**비추천:**
```swift
var colour = "red"
```

## Smiley Face

웃는얼굴이  raywenderlich.com사이트의 놀라운 스타일을 보여준다. 웃는 행복과 흥분을 가져다주는 미소임을 코딩주제로 매우 중요합니다. 닫힌 대괄호는 ‘]’을 사용합니다.
왜냐하면 ASCII아트를 사용하여 캡쳐할 수 있는 최대 미소를 나타낼 수 있기 때문입니다. 괄호는 ‘)’는 어중간한 미솔로 작성하기 때문에 바람직하지 않습니다.

**추천:**
```
:]
```

**비추천:**
```
:)
```  


## Credits

This style guide is a collaborative effort from the most stylish raywenderlich.com team members:

* [Soheil Moayedi Azarpour](https://github.com/moayes)
* [Scott Berrevoets](https://github.com/Scott90)
* [Eric Cerney](https://github.com/ecerney)
* [Sam Davies](https://github.com/sammyd)
* [Evan Dekhayser](https://github.com/edekhayser)
* [Jean-Pierre Distler](https://github.com/pdistler)
* [Colin Eberhardt](https://github.com/ColinEberhardt)
* [Greg Heo](https://github.com/gregheo)
* [Matthijs Hollemans](https://github.com/hollance)
* [Erik Kerber](https://github.com/eskerber)
* [Christopher LaPollo](https://github.com/elephantronic)
* [Andy Pereira](https://github.com/macandyp)
* [Ryan Nystrom](https://github.com/rnystrom)
* [Cesare Rocchi](https://github.com/funkyboy)
* [Ellen Shapiro](https://github.com/designatednerd)
* [Marin Todorov](https://github.com/icanzilb)
* [Chris Wagner](https://github.com/cwagdev)
* [Ray Wenderlich](https://github.com/rwenderlich)
* [Jack Wu](https://github.com/jackwu95)

Hat tip to [Nicholas Waynik](https://github.com/ndubbs) and the [Objective-C Style Guide](https://github.com/raywenderlich/objective-c-style-guide) team!

We also drew inspiration from Apple’s reference material on Swift:

* [The Swift Programming Language](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/index.html)
* [Using Swift with Cocoa and Objective-C](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/index.html)
* [Swift Standard Library Reference](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/SwiftStandardLibraryReference/index.html)
