---
title: "Go Methods"
date: 2023-01-03T22:54:11-05:00
draft: false
tags: ["go"]
---

Receivers are the variables a method gets access to when it runs.

    type foo struct {}
    func (o foo) someMethod() {}

The `(o foo)` is the receiver, and the `o` is the variable that let's the someMethod code do stuff with that instance of `foo`. You can have "pointer receivers" which means it would become `(o foo*)`. This let's use modify that instance of `foo`. There is some interplay with interfaces and pointer receivers.

Methods can be defined for either pointer or value receiver types.
Go automatically handles conversion between values and pointers for method calls.[^1]

    package main

    import "fmt"

    type rect struct {
        width, height int
    }

    func (r *rect) area() int {
        return r.width * r.height
    }

    func (r rect) perim() int {
        return 2*r.width + 2*r.height
    }

    func main() {
        r := rect{width: 10, height: 5}

        fmt.Println("area: ", r.area())
        fmt.Println("perim:", r.perim())

        rp := &r
        fmt.Println("area: ", rp.area())
        fmt.Println("perim:", rp.perim())
    }

## References
[^1]: Go by Example https://gobyexample.com/methods