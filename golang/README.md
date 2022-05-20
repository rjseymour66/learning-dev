# Project setup



# Arrays

## Internals

An array in Go is a fixed-length data type that contains a contiguous block of elements of the same type

Having memory in a contiguous form can help to keep the memory you use stay loaded within CPU caches longer
Since each element is of the same type and follows each other sequentially, moving through the array is consistent and fast

An array is declared by specifying the type of data to be stored and the total number of elements required, also known as the array’s length.
The type of an array variable includes both the length and the type of data that can be stored in each element

When you pass variables between functions, they’re always passed by value. When your variable is an array, this means the entire array, regardless of its size, is copied and passed to the function.
You can pass a pointer to the array and only copy eight bytes, instead of eight megabytes of memory on the stack
You just need to be aware that because you’re now using a pointer, changing the value that the pointer points to will change the memory being shared

```go
var array [5]int                        // standard declaration
array := [5]int{10, 20, 30, 40, 50}     // array literal declaration
array := [...]int{10, 20, 30, 40, 50}   // Go finds the length based on num of elements
array := [5]int{1: 10, 2: 20}           // initialize specific elements

// pointers
array := [5]*int{0: new(int), 1: new(int)}  // array of pointers
array2 := [3]*string{new(string), new(string), new(string)}
// dereference to assign values
*array[0] = 10
*array[1] = 20
*array2[0] = "Red"
*array2[1] = "Blue"
```

Once an array is declared, neither the type of data being stored nor its length can be changed
they’re always initialized to their zero value for their respective type

An array is a value in Go. This means you can use it in an assignment operation
```go
var array1 [5]string
array2 := [5]string{"Red", "Blue", "Green", "Yellow", "Pink"}
array1 = array2
```

# Slices

Slices are built around the concept of dynamic arrays that can grow and shrink as you see fit.

You can use the built-in function called append, which can grow a slice quickly with efficiency. You can also reduce the size of a slice by slicing out a part of the underlying memory

## Internals

Three fields of a slice:
- pointer to the underlying array
- length or number of elements the slice can access from the array
- capacity or number of els that the slice has available for growth

Trying to create a slice with a capacity that's smaller than the length is not allowed.

Remember, if you specify a value inside the [ ] operator, you’re creating an array. If you don’t specify a value, you’re creating a slice.

```go
array := [3]int{10, 20, 30}
slice := []int{10, 20, 30}
```

An idiomatic way of creating a slice is to use a slice literal
A nil slice is the most common way you create slices in Go. They can be used with many of the standard library and built-in functions that work with slices.
Empty slices are useful when you want to represent an empty collection, such as when a database query returns zero results

```go
slice := make([]string, 5)          // create a slice of strings with 5 capacity
slice := make([]int, 3, 5)          // length 3, cap 5

// Idiomatic slice literals
slice := []int{10, 20, 30}          // slice literal
slice := []string{99: ""}           // initialize the index that represents the length and capacity you need

// nil slice is created by declaring a slice without any initialization
var slice []int                     // nil slice

// empty slice
slice := make([]int, 3)             // empty slice with make
slice := []int{}                    // slice literal to create empty slice of integers
```

## Working with slices

When you make a slice of a slice, they share the same underlying array. You need to remember that you now have two slices sharing the same underlying array. Changes made to the shared section of the underlying array by one slice can be seen by the other slice.
A slice of a slice cannot access elements of underlying array that are prior to the pointer

Trying to access an element outside of its length will cause a runtime exception

To use append, you need a source slice and a value that is to be appended

When there’s no available capacity in the underlying array for a slice, the append function will create a new underlying array, copy the existing values that are being referenced, and assign the new value. So, if you append to the 3rd index of a slice with length 2, you get a new underlying array of length 3 with a capacity doubled the original array.

Capacity is always doubled when the existing capacity of the slice is under 1,000 elements

This third index gives you control over the capacity of the new slice. The purpose is not to increase capacity, but to restrict the capacity.

When you include a third value in the slice operation (`slice := source[2:3:4]`), the last value restricts the capacity. So this copies the element at index 2, and includes a capacity of 2 but does not copy the element in source[3].
Again, the first value represents the starting index position of the element the new slice will start with—in this case, 2. The second value represents the starting index position (2) plus the number of elements you want to include (1); 2 plus 1 is 3, so the second value is 3. For setting capacity, you take the starting index position of 2, plus the number of elements you want to include in the capacity (2), and you get the value of 4.
Once that capacity is reached, it will allocate a new underlying array
By having the option to set the capacity of a new slice to be the same as the length, you can force the first append operation to detach the new slice from the underlying array. Detaching the new slice from its original source array makes it safe to change.

```go
// Create a slice of strings.
// Contains a length and capacity of 5 elements.
source := []string{"Apple", "Orange", "Plum", "Banana", "Grape"}

// Slice the third element and restrict the capacity.
// Contains a length and capacity of 1 element.
slice := source[2:3:3]

// Append a new string to the slice. This doesn't change 'Banana' in the underlying array, it creates a new one
slice = append(slice, "Kiwi")
```

```go
// change value of slice
slice[1] = 25

// making a slice of a slice
slice := []int{10, 20, 30, 40, 50}
newSlice := slice[1:3]              // length 2, cap 4. 1 is the index position of the element that the new slice starts with
// Length:   3 - 1 = 2
// Capacity: 5 - 1 = 4

// append
newSlice = append(newSlice, 60)

// Slice the third element and restrict the capacity.
// Contains a length of 1 element and capacity of 2 elements.
slice := source[2:3:4]
```

The built-in function append is also a variadic function. Use the ... operator to append all the elements of one slice into another.
```go
s1 := []int{1, 2}
s2 := []int{3, 4}

// Append the two slices together and display the results.
fmt.Printf("%v\n", append(s1, s2...))

Output:
[1 2 3 4]
```

len returns the length of the slice, and cap returns the capacity:
```go
slice := []int{1, 2, 3, 4, 5}
length := len(slice)    // 5
capacity := cap(slice)  // 5?
```

## Iterating over slices

Use `for` with `range` to iterate over slices from the beginning:

```go
for index, value := range <slice-name> {
    fmt.Printf("index: %d, value: %d", index, value)
}

// discard the index with a '_'
for -, value := range <slice-name> {
    fmt.Printf("value: %d", value)
}
```

`range` returns the index and a copy of the value for each iteration, not a reference. Don't use pointers (`&value`) because its an address that contains the copy of the `value` that is being copied.

To iterate over a slice from an index other than 0, use a traditional for loop:

```go 
for i := 2; i < len(slice); i++ {
    fmt.Printf("index: %d, value: %d", index, slice[i])
}
```
### Passing slices between functions

Pass slices by value, because slices only contain a pointer to the underlying array, its length, and capacity. This is why slices are great--no need for passing pointers.

On 64-bit machines, each component of the slice requires 8 bytes (24 total).

```go
bigSlice := make([]int, 1e9)

slice = fName(slice)

func fName(slice []int) []int {
    return slice
}
```

# Maps

A map provides you with an unordered collection of key/value pairs. maps are unordered collections, and there’s no way to predict the order in which the key/value pairs will be returned because a map is implemented using a hash table
The map’s hash table contains a collection of buckets. When you’re storing, removing, or looking up a key/value pair, everything starts with selecting a bucket. This is performed by passing the key—specified in your map operation—to the map’s hash function. The purpose of the hash function is to generate an index that evenly distributes key/value pairs across all available buckets.

The strength of a map is its ability to retrieve data quickly based on the key. They do not have a capacity or a restriction on growth.
Use len() to get the length of the map
The map key can be a value from any built-in or struct type as long as the value can be used in an expression with the == operator. You CANNOT use:
- slices
- functions
- struct types that contain slices

## Creating and initializing

To create a map, use `make` or a map literal. The map literal is idiomatic:

```go
// create with make
dict := make(map[string]int)

// create and initialize as a literal IDIOTMATIC
dict := map[string]string{"Red": "#da1337", "Orange": "#e95a22"}

// slice as the value
dict := map[int]string{}

// assigning values with a map literal
colors := map[string]string{}
colors["Red"] = "#da137"

// DO NOT create nil maps, they result in a compile error
var colors map[string]string{}

```
## Testing if values exist in a map

Test with the following 2 options:
1. You can retrieve the value and a flag that explicitly lets you know if the key exists:
```go
value, exists := colors["Blue"]

if exists {
    fmt.Println(value)
}
```
2. Return the value and test for the zero value to determine if the key exists:
```go
value, exists := colors["Blue"]

if value != "" {
    fmt.Println(value)
}
```

## Iterating over maps with the for range loop

This works the same as slices, except index/value -> key/value:

```go
// Create a map of colors and color hex codes.
colors := map[string]string{
    "AliceBlue":   "#f0f8ff",
    "Coral":       "#ff7F50",
    "DarkGray":    "#a9a9a9",
    "ForestGreen": "#228b22",
}

// Display all the colors in the map.
for key, value := range colors {
    fmt.Printf("Key: %s  Value: %s\n", key, value)
}
```

Use the built-in function `delete` to remove a value from the map:

```go
delete(colors, "Coral")
```

## Passing maps to functions

Functions do not make copies of the map. Any changes made to the map by the function are reflected by all references to the map:

```go
func main() {
    // Create a map of colors and color hex codes.
    colors := map[string]string{
       "AliceBlue":   "#f0f8ff",
       "Coral":       "#ff7F50",
       "DarkGray":    "#a9a9a9",
       "ForestGreen": "#228b22",
    }

    // Call the function to remove the specified key.
    removeColor(colors, "Coral")

    // Display all the colors in the map.
    for key, value := range colors {
        fmt.Printf("Key: %s  Value: %s\n", key, value)
    }
}

// removeColor removes keys from the specified map.
func removeColor(colors map[string]string, key string) {
    delete(colors, key)
}
```

# Type system

Go is statically typed, which means that the compiler wants to know the type for every value in the program. This creates more efficient and secure code that is safe from memory corruption and bugs.

Types tell the compiler how much memory to allocate (its size) and what the memory represents. Some types get their representation based on the machine architecture (64- vs 32-bit).

## User-defined types

There are 2 ways to declare a user-defined type in Go:
1. Use the keyword `struct` to create a composite type:
```go
type user struct {
    name    string
    age     int64
    email   string
}
```
After you define the struct, you can declare a variable of the type with a value or zero value:
```go
// Idiomatic: declare zero-values with var
var bill user
```

You can also declare a struct literal, which is the declaration and values all in one:

```go
// add a comma after the last value
ryan := user{
    name:   "Ryan",
    age:    38,
    email:  "email@email.com",
}

// without the field names
ryan := user{"Ryan", 38, "email@email.com"}

// embedding user-defined types
type superuser struct {
    person      user
    password    string
}

boss := superuser{
    person: user{
        name:   "Ryan",
        age:    38,
        email:  "email@email.com",
    },
    password:   "pword",
}
```

2. Use an existing type as the specification for a new type:

```go
type Distance int64

// lets you add methods to a slice. This is useful when you want to decalure behavior around a built-in or refernce type
type List []string
```

## Methods

Methods add behavior to user-defined types:

```go
func (r receiver) fName(p params) {}
```

The receiver binds the function to the specified type to create a method for the type. How the receiver is declared determines how Go operates on the type value. There are 2 types of receivers:

1. value. When you declare a method using a value receiver, the method will always be operating against a copy of the value used to make the method call

If adding or removing something from a value of this type need to create a new value, then use value receivers for your methods.

```go
func (u user) sendEmail()
ryan := user{"Ryan", 38, "email@email.com"}
ryan.sendEmail()
```
You can also call methods that are declared with a value receiver using a pointer:
```go
func (u user) sendEmail()
ryan := &user{"Ryan", 38, "email@email.com"}
ryan.sendEmail()
```
Go adjusts (dereferences) the pointer value to comply with the method's receiver. So, `sendEmail()` is operating against a copy of the value that `ryan` points to.

2. pointer. When you call a method declared with a pointer receiver, the value used to make the call is shared with the method. Pointer receivers operate on the actual value, and any changes are reflected in the value after the call.

Generally, use pointers when you are using nonprimitive values.

If adding or removing something from a value of this type need to mutate the existing value, then use value receivers for your methods.

```go
func (u *user) changeEmail(email string) {
    u.email = email
}
ryan := &user{"Ryan", 38, "email@email.com"}
ryan.changeEmail("new@email.com")
```
You can also call methods that are declared with a pointer receiver using a value:
```go
func (u *user) changeEmail(email string) {
    u.email = email
}
ryan := user{"Ryan", 38, "email@email.com"}
ryan.changeEmail("new@email.com")
```
Go adjusts (dereferences) the pointer value to comply with the method's receiver. So, `sendEmail()` is operating against a copy of the value that `ryan` points to.

## Reference types
When you decalure a reference type, the value is a header value that contains a pointer to the underlying data structure. The header contains a pointer, so you can pass a copy of any reference type and share the underlying data structure.

The following are reference types:
- slice
- map
- channel
- function types

## Interfaces

Interfaces are types that declare behavior. They are implemented by user-defined types through methods. If a type implements an interface with a method, then a value of that user defined type can be assigned to values of the interface type.

Go uses implicit interfaces, which means that you do not have to declare that the method implements the interface, you just need to use the contract.

When you call a method that accepts an interface value, Go looks at the method set for the user-defined type and tries to find a method that implements the interface. The user-defined type is called the 'concrete type' because it provides the interface concrete behavior. For example:

```go 
// io.Reader interface
type Reader interface {
    Read(b []byte) (n int, err error)
}

// Stringer interface. `Stringer` is the name of the interface, and its signature is within the curly brackets. 
type Stringer interface {
    String() string
}
```
You can implement the `io.Reader` interface for a user-defined type if the function is:
- named `Read`
- accepts a slice of bytes ([]byte is a nil slice)
- returns an integer and an error

You can implement the `Stringer` interface if the function is:
- named `Stringer`
- returns a string


Interface values are two-word data structures:
1. A pointer to an internal table called iTable. iTable contains information about the user-defined stored value that implements the interface: the value's type and its list of methods.
2. A pointer to the actual stored value.

So, if you have a user that implements the `Stringer` interface:

```go
// user type
type user struct {
    name    string
    age     int64
    email   string
}


// user-defined interface 
type birthdater interface {
    birthday()
}

// user implements the Stringer interface
func (u user) String() string {
    return fmt.Sprintf("My name is %s", u.name)
}

// method with ptr receiver to update the user's email
func (u *user) updateEmail(newEmail string) {
    u.email = newEmail
}

// implement the birthdater interface
func (u *user) birthday() {
    u.age++
}

// user struct literal without field names
ryan := user{"Ryan", 38, "email@email.com"}
```
The Stringer iTable contains information about the user type, which includes its list of methods. It also contains a pointer to the memory address that stores the actual user value. You cannot swap value and pointer receiver semantics with interface implementation.

If you implement an interface using a pointer receiver, then only pointers of that type implement the interface:

```go

// user type
type user struct {
    name        string
    password    string
}

// superuser type
type superuser struct {
    person      user
    password    string
}

// user-defined interface 
type passUpdater interface {
    updatePassword(p string)
}

// user

```
