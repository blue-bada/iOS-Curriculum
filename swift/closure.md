# Closure

```swift
func printStudentNumber(message: String) -> (String) -> String {
    return { (number: String) -> String in
        return message + number
        
    }
}

let student = printStudentNumber(message: "학번 : ")
student("2016136121")
```



```swift
func printStudentNumber(message: String) -> (String) -> String {
    return { number in
        return message + number
    }
}

let student = printStudentNumber(message: "학번 : ")
student("2016136121")
```



```swift
func printStudentNumber(message: String) -> (String) -> String {
    return { 
        return message + $0
    }
}

let student = printStudentNumber(message: "학번 : ")
student("2016136121")
```



```swift
func printStudentNumber(message: String) -> (String) -> String {
    return { message + $0 }
}

let student = printStudentNumber(message: "학번 : ")
student("2016136121")
```



```swift
let printStudentNumber: (String, String) -> String = { $0 + $1 }
print(printStudentNumber("학번 : ", "2016136121"))
```









