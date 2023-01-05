---
title: "GOPL - Chapter 7 Interfaces"
date: 2023-01-02T15:25:30-05:00
draft: false
tags: [go]
---

## Interface Types

**Concrete Type** specifies the exact representation of its values and exposes the intrinsic operations of the representation.
	
**Interface Type** is an abstract type that doesn't expose the representation or internal structure of its values, or the set of basic operations they support; it reveals only some of their methods.

    type ReadWriter interface {
        Reader
        Writer
    }

The syntax above, which resembles struct embedding, lets us name another interface as a shorthand for writing out all of its methods. This is called *embedding* and interface.

## Interface Satisfaction

A type satisfies an interface if it possesses all the methods the interface requires. For example, *os.File satisfies `io.Reader`, `Writer`, `Closer`, and `ReadWriter`.

The assignability rule for interfaces is an expression may be assigned to an interface only if its type satisfies the interface.

A value of type T does not possess all the methods that a *T pointer does, and as a result it might satisfy fewer interfaces.

The type `interface{}`, is called the *empty interface* type, it places no demands on the types that satisfy it, we can assign any value to the empty interface.

## Interface Values

A value of an interface type, or interface value, has two components, a concrete type and a value for that type. These are called the interface's *dynamic type* and *dynamic value*.

Interface values may be compared using == and !=. Two interface values are equal if both are nil, or if their dynamic types are identical and their dynamic values are equal. Because interface values are comparable, they may be used as the keys of a map or as the operand of a switch statement.

However, if two interface values are compared and have the same dynamic type, but that type is not comparable (a slice, for instance), then the comparison fails with a panic.

Only compare interface values if you are certain that they contain dynamic values of comparable types.

During debugging, report the dynamic type of an interface value using fmt %T.

    var w io.Writer
    fmt.Printf("%T\n", w) // "<nil>"

    w = os.Stdout
    fmt.Printf("%T\n", w) // "*os.File"

A nil interface value, which contains no value at all, is not the same as an interface value containing a pointer that happens to be nil.

## Sorting

Go uses an interface, sort.Interface, to specify the contract between the generic sort algorithm and each sequence type that may be sorted.

An in-place sort algorithm needs three things.
1. The length of the sequence
2. A means of comparing two elements
3. A way to swap two elements

These are the methods fo sort.Interface:

    package sort

    type Interface interface {
        Len() int
        Less(i, j int) bool // i, j are indices of sequence elements
        Swap(i, j int)
    }

The Len and Swap methods have identical definitions for all slice types.

## The http.Handler Interface

Package net/http provides **ServeMux**, a request *multiplexer*, to simplify the association between URLs and handlers. A **ServeMux** aggregates a collection of http.Handlers into a single http.Handler.

For convenience, `net/http` provides a global `ServeMux` instance called `DefaultServeMux` and package-level functions called `http.Handle` and `http.HandleFunc`. To use DefaultServerMux as the server's main handler, we needn't pass it to ListenAndServe, `nill` will do.

    func main() {
        db := database{"shoes": 50, "socks": 5}
        http.HandleFunc("/list", db.list)
        http.HandleFunc("/price", db.price)
        log.Fatal(http.ListenAndServe("localhost:8000", nil))
    }

## Exercise 7.11
A handler request of /update?item=socks&price=6 to update the database. This introduces concurent variable updates.

    func (p *PriceDB) Update(w http.ResponseWriter, r *http.Request) {
        item := r.FormValue("item")
        if item == "" {
            http.Error(w, "No item given", http.StatusBadRequest)
            return
        }

        priceStr := r.FormValue("price")
        price, err := strconv.Atoi(priceStr)
        if err != nil {
            http.Error(w, "No integer price given", http.StatusBadRequest)
            return
        }

        if _, ok := p.db[item]; !ok {
            http.Error(w, fmt.Sprintf("%s doesn't exist", item), http.StatusNotFound)
            return
        }

        p.Lock()
        p.db[item] = price
        p.Unlock()
    }

## Excercise 7.12
html/template package to print the output as a HTML table

    var listHTML = template.Must(template.New("list").Parse(`
    <html>
    <body>
    <table>
        <tr>
            <th>item</th>
            <th>price</th>
        </tr>
    {{range $k, $v := .}}
        <tr>
            <td>{{$k}}</td>
            <td>{{$v}}</td>
        </tr>
    {{end}}
    </table>
    </body>
    </html>
    `))

    func (p *PriceDB) List(w http.ResponseWriter, r *http.Request) {
        p.Lock()
        listHTML.Execute(w, p.db)
        p.Unlock()
    }

## The `error` Interface

The `error` type is an interface type with a single method that returns an error message:

    type error interface {
        Error() string
    }

`syscall` package provides Go's low-level system call API. Defines a numeric type `Errno` that error method does a lookup in a table of strings. `Errno` is an efficient representation of system-call errors drawn from a finite set, and it satisfies the standard error interface.

The `go test` command runs a package's tests:

    $ go test -v gopl.io/ch7/eval

The -v flag lets us see the printed output of the test.

## Type Assertions
A type assertion is an operation applied to an interface value. A type assertion checks that the dynamic type of its operand matches the asserted type.

    x.(T)
`x` is an expression of an interface type and `T` is a type, called the **asserted** type.

If `T` is a concrete type, then the type assertion checks whether `x`'s dynamic type is *identical* to `T`.\
If `T` is an interface type, then the type assertion checks whether `x`'s dynamic type *satisfies* `T`.

## Terms

**&buf** Is a pointer to a memory buffer to which bytes can be written.

**Substitutabiliy** is freedom to substitute one type for another that satisfies the same interface.

**Interface Type** specifies a set of methods that a concrete type must posses to be considered an instance of that interface.

**Writter** is any types to which bytes can be written. (ex. files, memory buffers, network connections, HTTP clients, archivers, hashers)

**Reader** is any type from which you can read bytes.

**Closer** is any value that you can close. (ex. file or network connection)
