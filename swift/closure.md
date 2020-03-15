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

















