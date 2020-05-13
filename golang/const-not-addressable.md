# Cannot use the address operator on Const values

The Go language does not allow the `&` operator on const variables due to the following:

> 1. A constant may not have an address at all.
> 2. And even if a constant value is stored in memory at runtime, this is to help the runtime to keep constants that: constant. If you could take the address of a constant value, you could assign the address (pointer) to a variable and you could change that (the pointed value, the value of the constant). Robert Griesemer (one of Go's authors) wrote why it's not allowed to take a string literal's address: "If you could take the address of a string constant, you could call a function [that assigns to the pointed value resulting in] possibly strange effects - you certainly wouldn't want the literal string constant to change." (source)

This mean that to use a pointer to a const var you need to assign it to a var first and then use the address operator on it. Like so:

```go
func main() {
    const k = 5
    v := k
    address := &v // This is allowed
}
```

[More information on this well written Stack Overflow post](https://stackoverflow.com/questions/35146286/find-address-of-constant-in-go)
