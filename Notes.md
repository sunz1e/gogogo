# Notes from the perspective of java developer: 

- there are no semi-colons. 
- `import` is just a single statement. Looks like a function call but the params are package names you want to import and also the params are on each line and there are no commas between them.
- `import` can be multiple sentences as well but above way is present in go. 
- defining a function is by func. If it returns nothing you write nothing. 
- The access is based on casig of the start letter of the word. If the 
- Encapsulation is enforced based on the case of the first letter of the method, field, type. If the first letter is capital then its a public method and if its lower case its private only available within the package. 
- But multiple files can have same package so the boundary of the encapsulation is not same as the boundary of the file. 
- defining a function. func followed by the function name and the parameters are name followed with type. multiple params are separated by comma and the return type is given after the brackets but before the curly brackets. 
- you don't need to specify the type of all the params in the function def. If many params are sharing same type you define the type only for the last one in the order. 
- you can return multiple things in go. This is cute. you can define the return type as (string, string) and when you call the function you can recieve them like a, b := myFunction call. 
- = is for assignment of the value to a defined variable and := is to define and assign the value both. 
- oh yes, variables are just defined by just writing and using := for assignment. no need to provide a type for a constant and function results. but when you don't provide a constant or not recieving a function call you need to add var then name then type at the end of the variable. You can define multiple variables at once with same type as well. like var i, j int 
- you can initialize variables as well with the definition. var i, j int = 1, 2 
- this is weird thing. you can name variables when you define the return of the go function. Like instead of doing just (string, string) you could do (x,y string). This way you create new variables for the scope of your funtion and to return you just write return. no need to specify what to return because we already defined in the return of the function definition. 
- to return multiple things you just return them with comma separated manner. Be mindful that the order of the variables matter. 
- outside a function every definition should have var, func and so on so you cannot use :=. := is shorthand to define and assign. 
- basic types are bool, string, int, int8, int16, int32, int64, uint, uint8, uint16, uint32, uint64, uintptr, byte, rune, float32, float64, complex64, complex128 
- complex numbers are a type itself. int and int8 are different because int can be assigned 4 0r 8 bytes based on the system. 32bits or 64 bits respectively. uint means unsigned ints. uintptr is a type for storing memory address. 
- fields are initialized with 0, false and empty string if not initialized. 
- types expose funtions like uint() which can help with type conversion. like a constructor I feel. 
- constants are declare with `const`. cannot work with :=
- `const Big = 1 << 100`. It results in a very large value: `2^100`. In decimal, this is approximately `1,267,650,600,228,229,401,496,703,205,376`. The maximum size of an `int` depends on the platform. `2^100` exceeds both these limits, so it cannot fit in an `int`. Therefore, using `Big` in a context that requires an `int` (e.g., `needInt(Big)`) would result in a compile-time error. `Big` works as a `float64`. A `float64` can handle very large numbers because it uses scientific notation. `Big` (≈ 1.267 × 10^30) easily fits within the `float64` range . `return x * 0.1` results in: `2^100 * 0.1` ≈ `1.2676506002282295e+29`
- only `for` loop. `for i := 0; i < 10; i++ {` no parenthese required for the variables. variables have semi colon!!!
- it can be acting as a `while` loop without first and third component. `for ; sum < 1000; {` and you don't need to keep the ; then and directly write `for sum < 1000 {`
- this is an infinite loop `for {`
- just like if you don't need to put parenthese with `if` as well. But if we put it doesn't error out. 
- `if` is capable of something like `try with resources` of java. you can do something like `if v := math.Pow(x, n); v < lim` getting the variable and evaluating it too in if. This let us to define the scope of the variable only inside the `if`. 
- Variables declared inside an `if` short statement are also available inside any of the `else` blocks.
- `switch` statement is similar with the trigger just after `switch` keyword. Just like `for` and `if` it can have a short hand def and assignment of the trigger. cases are `case` keyword with the value following it. 
- cases can also have function call or an expression which needs to be evaluated. Switch cases evaluate cases from top to bottom, stopping when a case succeeds.
- without a condition/trigger the `switch` statement is like a `if else` chains. its like switch true. basically whichever case returns true you execute that hence like a chain of `if else`
- `defer` keyword. A defer statement defers the execution of a function until the surrounding function returns. So basically run the function I am in and then run this statement in a defered manner. 
- multiple `defer` are being executed in reverse order of their existence in the code. seems like stack mechanism is being used internally? Yes multiple defer statements in a function are executed in LIFO (Last-In, First-Out) order when the function returns.
- Go has pointers. Define one with `*T` for a type `T`. Variable which holds value to pointer: add `&`. Pointer to value: add `*` to the var.   
- `struct` is a collection of fields. if you want to define the structure you need to use `type name struct {` but you can also define anonymous `struct` like `v := struct { X int; Y int }{ X: 10, Y: 20 }`
- You can create instances of `struct` same way like `myStructWithTwoInts{1, 2}`. You can access the values with a dot. You could get the pointer of the struct and access the values with a dot. 
- You could also give only some values like `v2 = Vertex{X: 1}  // Y:0 is implicit` and `v3 = Vertex{}      // X:0 and Y:0`
- Arrays can be defined with `[size]T`. `[9]string` defines an array of size 9 of type string. `[]T` denotes a slice. 
- Slice is a dynamic array. Like list in java. we can create slice of an array by defining it first	`primes := [6]int{2, 3, 5, 7, 11, 13}` then doing `primes[1:4]`
- Slices are like references to arrays. Changing the elements of a slice modifies the corresponding elements of its underlying array.
- defining a struct's slice with elements as well. 	
```GO
s := []struct {
		i int
		b bool
	}{
		{2, true},
		{3, false},
		{5, true},
		{7, true},
		{11, false},
		{13, true},
	}
```
- A slice has both a length and a capacity. length is the length of the view and capacity is the size of the array it is pointing to. 
- Slice's low and high bound have default values. empty low means start and empty high means end. 
- Slice shares the array internally and it doesn't create new data structure. It can be seen by following. Slice is just a view not the actual structure on memory.  
```GO
func main() {
	s := []int{2, 3, 5, 7, 11, 13}
	printSlice(s)

	// Slice the slice to give it zero length.
	s = s[:0] // you are reducing the size and overriding it. but the array is still there. the slice still has the reference to that array. 
	printSlice(s)

	// Extend its length.
	s = s[:4] // since slice keeps the array reference when we do this it doesn't get away because of overriding of the s before printing in above step.
	printSlice(s)

	// Drop its first two values.
	s = s[2:]
	printSlice(s)
}
```
- zero value of a pointer and slice is `nil`. You can do the comparision also `s == nil`
- accessing the index is based on length not on the capacity of a slice. `b[3] = 3` will give error if its current length is less than 4 even if its capacity is more than 4. 
- to resize the slice to its capacity can be done by `b = b[:cap(b)]`
- there is a `make` method. `make([]int, 0, 5)`. Initializes the array with 0. Keeps the initial length as specified and capacity. If only passes one, length and capacity are same.
- if you try to slice a slice beyond its capacity it will throw error. 
- 2 dimensional slice 
```GO

	// Create a tic-tac-toe board.
	board := [][]string{
		[]string{"_", "_", "_"},
		[]string{"_", "_", "_"},
		[]string{"_", "_", "_"},
	}

    //  upper way is static definition. make can help us to define it in a dynamic way. 
	picSlice := make([][]uint8, dy)
	for y := 0; y < dy; y++ {
		picSlice[y] = make([]uint8, dx)
	}

```
- you can append to a slice. appends at the end? yes. `s = append(s, 2, 3, 4)` REF: https://go.dev/blog/slices-intro
- bigger array is allocated if backing array is small to acomodate all the elements being appended. 
- Iterating over slice is possible using `range` function which can be used like ` range mySlice` which basically returns two value. it returns `index` and `value` which is the copy of the element at that index. 
- `for i, _ := range pow` or `for _, value := range pow` to avoid the variable if they are not required. `for i := range pow` will only capture the first variable which is the index here. 
- cannot give variable to slice length. or array length. 
- Map in GO. you define the key and value type like `map[keyType]ValueType`. the not initialized value/ zero value of a map is nil. you cannot put a key in it. you need to initialize it using `make` function. `m = make(map[string]Vertex)`
- or you define and initialize like `map[string]string{ "key": "value"}` or if its a struct as value you could do it like this `map[string]myStruct{ "key": {1, "fieldOfMyStruct"} }` where our `struct` takes two fields of type int and string. 
- Map operations: write `m[key] = elem`, read `elem = m[key]`, delete `delete(m, key)` reading with two value assignment `elem, ok := m[key]`
- word count in go 
```GO

func WordCount(s string) map[string]int {
	ans := make(map[string]int)
	words := strings.Fields(s)
	for _, word := range words{
		v, ok := ans[word]
		if ok {
			ans[word] =  1 + v
		} else{
			ans[word] = 1
		}
	}
	return ans
}

```
- Functions are values too. They can be passed around just like other values.
- defining a function value ` fn func(float64, float64) float64`. defines a function which takes two float args and return one float. 
- following defines a function which takes a function which takes two `float` args and return a `float`  
```GO
func compute(fn func(float64, float64) float64) float64 {
	return fn(3, 4)
}

```
- Go has closures. Closure is a function which access a variable from outside of its body. 
```GO
func adder() func(int) int {
	sum := 0
	return func(x int) int {
		sum += x
		return sum
	}
}
```
- fibonacci in go using closures 
```GO
func fibonacci() func() int {
	first, second := 0, 1
	return func () int{
		ans := first 
		first = second 
		second = first + ans
		return ans			
	}
}
```
- Creating methods for the structs. Go doesn't have classes but you can attach methods to the structs. When you do so you add a `receiver` to the method. which is basically reference to the struct this method being called upon. 
- You add a `receiver` to the method by add it as a param after `func` keyword and before method's name and params. for example. `func (v Vertex) Abs() float64` is a method with a `receiver` of type `Vertex` and it takes not arg and returns a `float`.
- inside the method. you can access the `struct` which is calling this method using `v` but you can only read the values. if you need to change the receiever you must get the pointer type. 
- like this `v := Vertex{3, 4} and v.Abs()`
- Methods are just functions with a receiver. you could write a function like `func Abs(v Vertex) float64` but then you would do `Abs(v)` not `v.Abs()`
- You can declare a method on non-struct types, too. for example for a `float`. Notice that we first define a type of float and then we define a method on it. 
```GO
type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

```
- Pointer receivers. You define the pointer receiver when you want to mutate the receiver inside your method. 
- this is because the method operates on the copy of he receiver. So actually change the receiver you should operate on a pointer to the receiver type. 
- method and functions which take pointers. when you create a function which takes a pointer argument you always need to pass pointer to the method call. But when you create a method with pointer receiver. You will call the method on the type's value the receiver pointers gets injected into the method call automatically. for example for `func (v *Vertex) Scale(f float64)`, `v.Scale(5)` is same as `(&v).Scale(5)` and we don't need to do it. Go handles it
- this is supported in reverse as well. if method takes a value, even then we can call method using pointer to the value of the same type for which method receiver is defined. 
- Using a pointer receiver is better because we can modify the actual value not the copy and it avoids creation of copy so less memory in case we are dealing with large structs. 
- ALL THE METHOD OF A GIVEN TYPE MUST BE EITHER POINTER RECEIVER OR VALUE NOT MIX. 
- `type` keyword in go. `type` keyword creates a new type. Creating a type definition basically. you use it like `type nameOfMyType andStructureOfThisType`. You give name of the type and the underlying structure you want your type to have. Now, Your type can have anything as underlying structure. For example when you do `type MyFloat float64` you are basically keeping `float64` as the underlying structure. 
- When you define a struct you basically define a custom type with struct as the underlying structure. 
```GO
type Vertex struct {
  X int
  Y int
}

```
- `interface` type in go. `interface` means collection of methods. You can define interface types which couple of methods without body like following: 
```GO
type myInterface interface {
	
	method1() float64
	method2() float64

}

```

- implementing an `interface` in go. You don't write code to show that your `type` is implementing this interface like Java. So you can define your type and you won't have any idea which interface it implements. 
- How do we connect the `interface` to my custom `type` which provides the implmentation of the methods? we do it by declaring a variable of our `interface` type and then we create a custom `type` which provides `method` with receivers where method names are same as the methods defined inside the `interface`. 
- example: 
```GO

type MyFloat float64

func (f MyFloat) method1() float64 {
	......
}

func (f MyFloat) method2() float64 {
	......
}

// here MyFloat implements both the methods of myInterface but there is no linking yet
```
- only when you will do the following
```GO
var a myInterface
a = MyFloat(1.4444)
``` 
- you are basically linking a reference of type myInterface to the actual implementations. So if you switch the type on right hand side you will switch the implementations as well. this is called implicit intent in go where the type implementing the interface doesn't explicitly say that hey I am implementing this interface. 
- IF YOUR CUSTOM TYPE DOESN'T IMPLEMENT ALL THE METHODS DEFINED IN INTERFACE YOU WILL GET ERROR DURING THIS ASSIGNMENT WHICH IS ACTUALLY LINKING THE INTERFACE AND THE IMPLEMENTATIONS. 
- Linking assignment does a hard check on receiver. So if the required method implementation has pointer receiver but you are trying to link a value type to the `interface` var. you will get error. 
```GO

// if we have 
type MyFloat float64

func (f *MyFloat) method1() float64 {
	......
}


// we can call 
c := MyFloat(1.44)
c.method1()
// even though the method is defined for pointer receiver. 

// but you cannot do this 

var a myInterface 
a = c

// where 
type myInterface interface {
	
	method1() float64
}

// because the method is defined for the pointer receiver. not the value type. 

// this works 
a = &c
```
- interface values. interfaces values have two parts to it. actual value and the type. we can use `describe` method defined below. it prints the actual value and the type tuple. 

```Go

type I interface {
	M()
}

type T struct {
	S string
	t string
}

func (t *T) M() {
	fmt.Println(t.S)
}

func describe(i I) {
	fmt.Printf("(%v, %T)\n", i, i)
}

var i I

i = &T{"Hello", "world"}

describe(i) // prints (&{Hello world}, *main.T)

```
- Different states of the variables of types an interface and a custom type. and their nil values
```Go
// you define interface
type I interface {
	M()
}

// you define custom type 
type T struct {
	S string
}

// and you link the type to interface by implementating the method 

func (t *T) M() {
	if t == nil {
		fmt.Println("<nil>")
		return
	}
	fmt.Println(t.S)
}

// when you only define a var which is of type interface
	var i I
// and you describe this 
	describe(i)
// prints (<nil>, <nil>)


// when you only define a var which is of your custom type
	var t *T
// and you describe this 
	describe(t)
// prints (<nil>, *main.T) value is still nill


// when you assign this to interface var and describe it also has value nill but now gets a type
	i = t
	describe(i)
// prints (<nil>, *main.T) value is still nill

i = &T{"hello"}
describe(i)
// prints (&{hello}, *main.T)

```









    