# Pre-Reading Notes
## Swift reading from Apple
### Simple Values
* `let` makes a constant
* `var` for a variable

Constants and variables must have the same type as the value you assign to them.

```swift
let implicitDouble = 70.0
let explicitDouble: Double = 70   // 70.0
```

Convert values explicitly or interpolate:

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width) // the width is 94
let widthLabel2 = "the width is \(width)" // same
```


Arrays and dictionaries use brackets and can access via index/key:

```swift
let emptyArray = [String]()
let emptyDictionary = [String: Float]()

// or even if type can be inferred
shoppingList = []
occupations = [:]
```

### Control Flow

```swift
for score in individualScores {
  if score > 50 {
    teamScore += 3
  } else {
    teamScore += 1
  }
}
```

Assign vars/constants with control flow:

```swift
if let name = optionalName {
  greeting = "Hello, \(name)"
} else {
  greeting = "buenos dias"
}
```

Case statements does not require a break statement (note the required default
case):

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
  let vegetableComment = "Add some raisins and make ants on a log."
case "cucumber", "watercress":
  let vegetableComment = "That would make a good tea sandwich."
case let x where x.hasSuffix("pepper"):
  let vegetableComment = "Is it a spicy \(x)?"
default:
  let vegetableComment = "Everything tastes good in soup."
}
```

Loops can be written with range or with init, condition, increment statements:

```swift
var firstForLoop = 0
for i in 0..<4 {
  firstForLoop += i
}
println(firstForLoop)

var secondForLoop = 0
for var i = 0; i < 4; ++i {
  secondForLoop += i
}
println(secondForLoop)
```

> Use `..<` to make a range that omits its upper value, and use `...` to make a
range that includes both values.


### Functions and Closures
* declare a function unsing `func`
* invoke a function using `()`
* separate params from function's return type with `->`

```swift
func greet(name: String, day: String) -> String {
  return "Hello \(name), today is \(day)."
}
greet("Bob", "Tuesday")
```

The return value can also be a tuple to return multiple values/types:

```swift
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
  //do stuffs
  return (min, max, sum)
```

Functions can also take a variable number of arguments:

```swift
func sumOf(numbers: Int...) -> Int {
  var sum = 0
  for number in numbers {
    sum += number
  }
  return sum
}
```

> Functions can be nested. Nested functions have access to variables that were
declared in the outer function.  


Functions are first class and can, therefore, return functions and accept
functions as arguments:

```swift
func makeIncrementer() -> (Int -> Int) {
  func addOne(number: Int) -> Int {
    return 1 + number
  }
  return addOne // returns inner function
}
var increment = makeIncrementer()
increment(7)


func hasAnyMatches(list: [Int], condition: Int -> Bool) -> Bool {
  for item in list {
    if condition(item) {
      return true
    }
  }
  return false
}
func lessThanTen(number: Int) -> Bool {
  return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(numbers, lessThanTen) // passes function as a param
```
