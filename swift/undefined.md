# 함수

```swift
func multiple(X: Int) -> Int {
    return X * 2
}

print(multiple(X: 4))  // 8
```



```swift
func multiple(input x: Int) -> Int {
    return x * 2
}

print(multiple(input: 8))  // 16
```



```swift
func multiple(_ x: Int) -> Int {
    return x * 2
}

print(multiple(8))  // 16
```



```swift
func multiple(x: Int = 4) -> Int {
    return x * 2
}

print(multiple())       // 8
print(multiple(x: 8))   // 16
```



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





