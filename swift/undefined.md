# 함수

기본적인 함수 형태

```swift
func multiple(X: Int) -> Int {
    return X * 2
}

print(multiple(X: 4))  // 8
```

함수 내 변수 명을 변경하고 싶은 경우

```swift
func multiple(input x: Int) -> Int {
    return x * 2
}

print(multiple(input: 8))  // 16
```

함수에서 변수 명을 생략하고 싶은 경우

```swift
func multiple(_ x: Int) -> Int {
    return x * 2
}

print(multiple(8))  // 16
```

함수에서 변수의 기본 값을 설정하고 싶은 경우

```swift
func multiple(x: Int = 4) -> Int {
    return x * 2
}

print(multiple())       // 8
print(multiple(x: 8))   // 16
```

함수에서 변수의 갯수를 가변으로 설정해야하는 경우

```swift
func multiples(_ numbers: Int...) -> Int {
    var multiple = 1
    for number in numbers {
        multiple *= number
    }
    return multiple
}

print(multiples(5,4,2))  // 40
```

함수에 함수를 변수로 넣는 방법 \( Closure와 연계해 진행\)

```swift
func printStudentNumber(message: String) -> (String) -> String {
    func student(number: String) -> String {
        return message + number
    }
    return student
}

let student = printStudentNumber(message: "학번 : ")
student("2016136121")
```





