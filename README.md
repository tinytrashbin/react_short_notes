# Learning ReactJS by Examples


## Start with local npm setup.

Step1: Install node.js and npm. Figure out the details of node.js installation from external sources.

Step2: Clone [this repo](https://github.com/tinytrashbin/react_app_with_flask_backend) to start with.

Step3: Go to cloned folder and run `npm install`.


### 1). Basic Example

Replace the content of **File: src/example3.jsx** by this content:

```JSX
import React from 'react';

function Example3(props) {
  return <h1>Hello World!</h1>;
}
```

and run: `localhost:3000/#/example3` , you will see `Hello World` in browser.

-----------------------------------

### 2). Expression evaluation inside HTML using `{...}`.

**File: src/example3.jsx**

```JSX
function Example3(props) {
  var name = "Truck"
  return <h1>Hello {name} ! There are total of {3 + 4} people.</h1>;
}
```

**React vs AngularJS Difference:**

1. `{name}` vs `{{name}}`
2. `{3 + 4}` vs `{{3 + 4}}`

-----------------------------------


### 3). Nested HTML Content

**File: src/example3.jsx**

```JSX
function Example3(props) {
  const name = "World"
  const what_i_like = "fruits"
  return (
    <div>
      <div>
          Hello {name}!
      </div>
      <div>
        <div>I like following {what_i_like}:</div>
        <ul>
          <li>Apples</li>
          <li>Bananas</li>
          <li>Cherries</li>
        </ul>
      </div>
    </div>
  );
}
```

-----------------------------------

### 4). Inline Style

React Syntax: `style={dict_expression}`

React Example1: `style={{color: "red", fontSize: "14px"}}`

AngularJS Syntax1 `ng-style="dict_expression"`

AngularJS Syntax2 `style="color: red; ...."`

AngularJS Example1: `ng-style="{color: 'red', 'font-size': '14px'}"`

**File: src/example3.jsx**

```JSX
function Example3(props) {
  const name = "World"

  const my_favorite_color = "blue"

  const my_weight = 80

  const pizza_color = (my_weight > 50 ? "lightblue": "red")

  var banana_style_dict = {fontSize: "14px"}
  banana_style_dict.fontWeight = 600
  banana_style_dict.border = "solid red 1px"
  if (my_weight > 80) {
    banana_style_dict.color = "red"
  } else {
    banana_style_dict.color = "brown"
  }

  return (
    <div>
      <div style={{color: "green", fontWeight: 900}} >
          Hello {name}!
      </div>
      <div>
        <div style={{color: my_favorite_color, fontSize: "15px"}} >I like following things:</div>
        <ul>
          <li>Apples</li>
          <li style={{color: pizza_color, fontSize: "16px"}} >Pizza</li>
          <li style={{color: (my_weight > 60 ? "blue": "red"), "padding": "20px 0px"}} >Cherries</li>
          <li style={banana_style_dict} >Banana</li>
        </ul>
      </div>
    </div>
  );
}
```

-----------------------------------

### 5). OnClick

React Syntax1: Function without argument: `onClick={func_name}`

React Syntax2: Function with argument: `onClick={() => func_name(x, y)}`

AngularJS Syntax1: `ng-click="func_name()"`

AngularJS Syntax2: `ng-click="func_name(x, y)"`

**File: src/example3.jsx**

```JSX
function Example3(props) {
  const func1 = function() {
    alert("Abc")
  }

  const func2 = function(x, y) {
    alert("Abc " + x + "," + y)
  }

  return (
    <div>
      <div><button onClick={func1} >Click1</button> </div>
      <div><button onClick={() => func2(4, 5)} >Click2</button> </div>
    </div>
  );
}
```

-----------------------------------

### 6). Conditionals / ng-if

React Syntax: `{condition && <div>....</div>}`

AngularJS Syntax: `<div ng-if="condition" >....</div>`

**File: src/example3.jsx**

```JSX
function Example3(props) {
  const animals = ["Cat", "Tiger"]
  const show_fruits = false
  return (
    <div>
      <div style={{border: "solid blue 1px"}} >
        Box1:
        {show_fruits && (
          <ul>
            <li>Apples</li>
            <li>Bananas</li>
            <li>Cherries</li>
          </ul>)}
      </div>
      <div style={{border: "solid blue 1px"}} >
        Box2:
        {animals.length > 0 && (
          <ul>
            <li>Cat</li>
            <li>Tiger</li>
          </ul>)}
      </div>
    </div>
  );
}
```

-----------------------------------

### 7). Map / ng-repeat

React Syntax: `{list.map((x) => <div>...{x}...</div>)}`

React Syntax (Advance): `{list.map((x) => <div key={some_unique_id} >...{x}...</div>)}`

AngularJS Syntax: `<div ng-repeat="x in list" >...{{x}} .</div>`

**File: src/example3.jsx**

```JSX
function Example3(props) {
  var fruits = ["Apple", "Banana", "Orange"]
  return (
    <div>
      <ul>
        {fruits.map((fruit) => (
          <div key={fruit} >
            I like <b>{fruit}</b>
          </div>
        ))}
      </ul>
    </div>
  );
}
```

Note:

1). It's optional to pass a `key` attribute when repeating a div. If we pass, it improves the speed/performance of application. we can pass a unique id or any other unique value.

-----------------------------------

### 8). State management and react hooks

If non-const variables (i.e. variables whose value can change over time) are used in HTML content, they should be used with state managers, like `useState` hook, `userImmer` hook, redux store etc.

In React, there are so many ways of managing state. Two main ways are `React.useState` and `useImmer` hooks.

#### 8.A). `React.useState` (Available with React by default)

- Suitable for Atomic types. Example: integers, boolean and string.
- Not suitable for complex types like list and dict. We must use `useImmer` hook for them.
- Suitable for complex types like list/dict **ONLY IF** we never edit them partially, but replace them with a new value.

How to use `React.useState`:

```JSX
// 10 is the initial value of variable `count`.
const [count, setCount] = React.useState(10);

// Using it's value. Which is 10.
<h1>{count}</h1>

// Change it's value to something else (100 in this case).
setCount(100);

// NOT ALLOWED.
count = 100;
```

Using complex type with `React.useState`:


```JSX
// This dictionary `{name: "A", ...}` is the initial value of variable `info`.
const [info, setInfo] = React.useState({name: "A", age: 40})
```

```JSX
// Using it's value.
<div>Name = {info.name}, Age = {info.age}</div>
```

```JSX
// Updating it's value to some other dictionary:
setInfo({name: "B", age: 55})
```

```JSX
// Updating it's value to some other dictionary:
setInfo(new_info)
```

```JSX
// NOT ALLOWED.
info.name = "B"
```

-----------------------------------

`React.useState` Example:

```JSX
function Example3() {
  const [name, setName] = React.useState("Alan")
  const [city, setCity] = React.useState("B")
  return (
    <div style={{border: "solid red 1px"}} >
      <div>My Name = {name} </div>
      <div>
        <input value={name} onChange={(e) => setName(e.target.value)} />
      </div>
      <div>My City = {city}</div>
      <div>
        <select value={city} onChange={(e) => setCity(e.target.value)} >
          <option>A</option>
          <option>B</option>
          <option>C</option>
        </select>
      </div>
    </div>
  );
}
```


#### 8.B) `useImmer` hook (Custom Implementation):

[This is a basic example](https://github.com/tinytrashbin/react_examples/blob/master/src/example2.jsx), demonstrating how `useImmer` hook can be used for state management.

Also See [Live demo (Example2)](https://tinytrashbin.github.io/react_examples/demos/#/example2)

**File: src/example2.jsx**

```JSX

function Example2() {
  const [books, setBooks] = useImmer([
      {id: 1, is_open: true, price: 100},
      {id: 2, is_open: false, price: 200},
      {id: 3, is_open: true, price: 300},
    ])
  const [idCounter, setIdCounter] = React.useState(4)

  const open = function(book_index) {
    setBooks(draft => {
      draft[book_index].is_open = true
    })
  }

  const close = function(book_index) {
    setBooks(draft => {
      draft[book_index].is_open = false
    })
  }

  const add = function() {
    setBooks(draft => {
      draft.push({id: idCounter, is_open: false, price: 80})
    })
    setIdCounter(idCounter + 1)
  }

  const increase_price = function(book_index, price) {
    setBooks(draft => {
      draft[book_index].price += price
    })
  }

  return (
    <div >
      <Header/>
      <h2>Example2</h2>
      <div className="top_box" >
        {books.map((book, book_index) => (
          <div key={book.id} style={{border: "solid red 1px", padding: "10px"}} >
            Book-{book.id}
            <div>{book.is_open ? "Open" : "Close"} ; Price = {book.price}</div>
            <button onClick={() => open(book_index)} >Open</button>
            <button onClick={() => close(book_index)} >Close</button>
            <button onClick={() => increase_price(book_index, 100)} >
              Increase Price
            </button>
          </div>
        ))}
      </div>
      <button onClick={add} >Add</button>
    </div>
  );
}

```

Note: When using `useImmer` hook, we need to call `updateState` like this only for updating the state. We cannot update the state directly.


-----------------------------------

### 11). API call and `React.useEffect` hook

Note: `Example3` function is called everytime state is changed. If a code needs to be executed only once (example: API call), it should be kept inside `React.useEffect` with second argument = `[]`

Syntax:

```JSX
React.useEffect(() => {
  // Any Code.. Example API call.
}, [])
```

**File: src/example3.jsx**

```JSX

function Example3(props) {
  const [name, setName] = React.useState("")
  const [count, setCount] = React.useState(0)

  var increment = function() {
    setCount(count + 1)
  }

  // this console.log will be there every time state is changed.. For
  // example when button is clicked.
  console.log("Inside Example3 " + count)

  React.useEffect(() => {
    // this console.log will be there exactly once.
    console.log("Inside React.useEffect")
    // This API takes 5 seconds to respond.
    api("/sleep_for_5_seconds_and_return_name", {}, function(backend_output) {
      setName(backend_output.name)
    })
  }, [])

  return (
    <div>
      <h2>Name = {name}</h2>
      <div>This API takes 5 seconds to respond. After 5 seconds name will be changed.</div>
      <div style={{fontSize: "20px"}} >Counter Value = {count}</div>
      <div>
        <button onClick={increment} >Click to Increase Counter</button>
      </div>
    </div>
  );
}

```

-----------------------------------

### 12). Subcomponents

Consider this example of building a house using smaller components:

**File: src/example3.jsx**

```JSX

function Window(props) {
  const style_dict = {
    display: "inline-block",
    width: "100px",
    height: props.height+ "px",
    border: "solid #ccc 1px",
    margin: "5px"
  };
  return (<div style={style_dict} >Window of {props.height}px height.</div>);
}

function Door() {
  const style_dict = {
    display: "inline-block",
    width: "100px",
    height: "200px",
    border: "solid red 1px",
    margin: "5px"
  };
  return (<div style={style_dict} >Door.</div>);
}

function Room1() {
  return (
    <div style={{border: "solid blue 1px", margin: "15px", display: "inline-block"}} >
      <h3>I am Room1</h3>
      <div >
        <Window height={100} />
        <Door/>
        <Window height={100} />
      </div>
    </div>
  )
}

function Room2() {
  return (
    <div style={{border: "solid blue 1px", margin: "15px", display: "inline-block"}} >
      <h3>I am Room2</h3>
      <div >
        <Window height={80} />
        <Window height={120} />
        <Door/>
        <Window height={120} />
        <Window height={80} />
      </div>
    </div>
  )
}

function Foodbox({name, quantity}) {
  return (
    <div style={{margin: "4px", backgroundColor: "#ddd"}} >
      I am {name}. My quantity = {quantity}kg.
    </div>
  )
}

function Kitchen() {
  const food_list = ["Apple Juice", "Paneer", "Paratha"]
  return (
    <div style={{border: "solid blue 1px", margin: "15px", display: "inline-block"}} >
      <h3>I am Kitchen</h3>
      <div>
        Food items:
      </div>
      <div>
        {food_list.map(food_name => <Foodbox name={food_name} quantity={2} />)}
      </div>
    </div>
  )
}

function Example3() {
  return (
    <div style={{border: "solid black 1px"}} >
      <Room1 />
      <Kitchen />
      <Room2 />
    </div>
  )
}

```

Note:

1). Parameters/arguments/attributes passed to a component can be accessed from `props` dictionary.

In this example, see how `height` is passed to `<Window height={80} />`
and how `name` is passed to `<Foodbox name={food_name} />`.

Which is then accessed using `props.height` or `props.name` in those component implementation.

2). In a component implementation, if inputs are declared like `function Foodbox({name, quantity}) {`, we can directly use the variable `name` and `quantity`.. because dictionary value coming from input is destructured into these 2 variable. [Learn more here](https://www.w3schools.com/react/react_es6_destructuring.asp).

[Example12 Demo](demos/example12)


-----------------------------------


### 13). [Advance] Custom onChange

Calling a function when value of a state variable is changed:

Syntax: 

```JSX
React.useEffect(() => {
  // Action to be taken when variables are changed.
}, [changed_variables])
```

In this example `age` is the changed variable.

**File: src/example3.jsx**

```JSX
function Example3(props) {
  const [age, setAge] = React.useState(20)
  const [remaining_age, setRemainingAge] = React.useState(80)

  React.useEffect(() => {
    setRemainingAge(100 - age)
  }, [age])

  return (
    <div style={{border: "solid red 1px"}} >
      <div>Age = {age} </div>
      <div>Remaining Age = {remaining_age} </div>
      <div>
        <input type="number" value={age} onChange={e => setAge(e.target.value)} />
      </div>
    </div>
  );
}
```

In this example, when `age` is changed, we want to update the `remaining_age` variable automatically.

Note: `React.useEffect` is same as what we used in Example11 for API call. In that example we passed `[]` second argument. If we pass `[]` as second argument then the `effect` will take place only once.

-----------------------------------

### Functions in JSX

```JSX
function Func1(x) {
  return x+2
}

var Func2 = function(x) {
  return x+2
}

var Func3 = (x) => {
  console.log(x)
  return x+2
}

// If the function has ONLY one statement, and the statement returns a
// value, you can remove the brackets and the return keyword.
var Func4 = (x) => x+2

// If you have ONLY one parameter, you can skip the parentheses as well:
var Func5 = x => x+2

// If function doesn't take any input.
var Func6 = () => 33
```

-----------------------------------

### Variables in JSX

```JSX
var x1 = 5.6;
var x2 = 5;

x1 = 88  // Ok. Allowed.

const y1 = 5.6;
// y1 = 6; // Not allowed. Error.

let z1 = "Abc"
z1 = "Def" // OK. Allowed.

function Func() {
  {  // Scope-1 Started.
    var p1 = 30
    let q1 = 60
    { // Scope-2 Started.
      console.log(p1) // Ok. Allowed.
      console.log(q1) // Ok. Allowed.
    }  // Scope-2 Ended.
    p1 += 1
    q1 += 1
    console.log(p1) // Ok. Allowed.
    console.log(q1) // Ok. Allowed.
    { // Scope-3 Started.
      console.log(p1) // Ok. Allowed.
      console.log(q1) // Ok. Allowed.
    }  // Scope-3 Ended.
    p1 += 1
    q1 += 1
  }  // Scope-1 Ended.
  console.log(p1) // Ok. Allowed. Prints 32.
  console.log(q1) // Not Allowed. Error "q1 undefined".
}
```

`q1` was defined inside `Scope-1`, hence it cannot be used once `Scope-1` ends.

`p1` can be used anywhere in function `Func`.

-----------------------------------

### JSX Syntax Requirements:

#### 1). Unpaired tags (example `<input />`, `<br/>`) must end with `/>`

Example:

 - Invalid: `<input>`

 - Valid: `<input/>`

 - Invalid: `<br>`

 - Valid: `<br/>`


#### 2). `className` instead of `class`

Example:

 - Invalid: `<div class="product_div" >Abc</div>`

 - Valid: `<div className="product_div" >Abc</div>`

 - Valid: `<div className={"product_div"} >Abc</div>`


#### 3). Only One Top Level Element.

Alternatively `<>`, `</>` can be used
   for avoiding unnecessary tags. This is called React Fragment.

Example:

- A). Invalid:

```JSX
function Example3(props) { // Error.
  return (
    <div>Abc</div>
    <div>Def</div>
  );
}
```

- B). Valid:

```JSX
function Example3(props) {
  return (
    <div>
      <div>Abc</div>
      <div>Def</div>
    </div>
  );
}
```

- C). Valid:

```JSX
function Example3(props) {
  return (
    <>
      <div>Abc</div>
      <div>Def</div>
    </>
  );
}
```

#### 4). `JSON.stringify` variables to show inside HTML.

By default an integer or string type of variable can be displayed in HTML using `{variable}`.

To display other type of variables (example - boolean, or list/dict) inside HTML, use `{JSON.stringify(variable)}`

```HTML
<div>List = {JSON.stringify(list)}</div>
```

### 15). React Router

React Router is useful for connecting URLs with different components.

For example, in this [Live demo](https://tinytrashbin.github.io/react_examples/demos/#/example2), we can see `Example1`, `Example2`, `Example3` shows up for different URL (on different tabs).

[From here](https://github.com/tinytrashbin/react_examples/tree/master/src) we can see that `Example1`, `Example2` and `Example3` are 3 different components defined in 3 different files.

Which are combined in [`common.jsx`](https://github.com/tinytrashbin/react_examples/blob/master/src/common.jsx)

**File: src/common.jsx**

```JSX
import Example1 from './example1';
import Example2 from './example2';
import Example3 from './example3';
import {Routes, Route, HashRouter} from "react-router-dom"

function Example3() {
  return (
    <HashRouter>
      <Routes>
        <Route >
          <Route path="/" element={<Example1 />} />
          <Route path="/example1" element={<Example1 />} />
          <Route path="/example2" element={<Example2 />} />
          <Route path="/example3" element={<Example3 />} />
          <Route path="*" element={<h1>Invalid</h1>} />
        </Route>
      </Routes>
    </HashRouter>);
}

export default Example3;
```

- As per these route declaration, when URL ends with `"/example2"`, then `Example2` component will display. Similarly for `Example1` and `Example3`.

- In real web applications, `Example1`, `Example2`, `Example3` are different page of website. For example: login page, signup page, profile page, admin page etc.



## JSX and modern JavaScript functions


- Which version of React are you using

> v-18

- Which version of HTML are you using ?

> HTML-5

- Which version of CSS are you using ?

> CSS-3

- Which version of JavaScript (ES) are you using ?

> ES6 (JavaScript/ES Latest Version). ES is the shortcut for ECMAScript. ECMAScript is old name of JavaScript.



> What is extra in ES6 ?

1). Advance feature like: function arrow (`x  => x+1`)

2). List spreading:

`New_list = [...list1, …list2, x, 44, ...list3]`


### Spread Operator (List)

```JSX
const list1 = [1, 2, 3];
const list2 = [5, 6, 7];
const list3 = [51, 61];
const x = 50;
const y =  [...list1, ...list2, x, 44, ...list3]
```

Value of `y` would be `[1, 2, 3, 5, 6, 7, 50, 44, 51, 61]`


```JSX
const z =  [...list1, list2, x, 44, ...list3]
```

Value of `z` would be `[1, 2, 3, [5, 6, 7], 50, 44, 51, 61]`


### Spread Operator (Dict)

```JSX
const d1 = {a: 10, b: 20}
const d2 = {...d1, c: 40}
```

Value of `d2` would be `{a: 10, b: 20, c: 40}`


### list.slice

```JSX
l=[10, 20, 30, 40, 50, 60, 70, 80]
l.slice(3, 6)
// Output would be [40, 50, 60] and it will NOT change original list.
```

### list.splice

Can be used for deleting an element of list or inserting item in a list.

A. Deleting item in a list:

```JSX
l=[10, 20, 30, 40, 50, 60]
l.splice(3, 1)
// Output is not important but the original list is changed now to [10, 20, 30, 50, 60]
// i.e. the item at index-3 is deleted.
// In `l.splice(3, 1)`, second arg 1 means 1 element is deleted.
```

B. Inserting item in a list:

```JSX
l=[10, 20, 30, 40, 50, 60]
l.splice(3, 0, 100)
// Output is not important but the original list is changed now
// to [10, 20, 30, 100, 40, 50, 60]
// i.e. the value 100 is inserted to take index-3.
// In `l.splice(3, 0, 100)`, second arg 0 means 0 elements were deleted.
```

C. Inserting multiple items in a list:

```JSX
l=[10, 20, 30, 40, 50, 60]
l.splice(3, 0, 100, 1000, 10000)
// Output is not important but the original list is changed now
// to [10, 20, 30, 100, 1000, 10000, 40, 50, 60]
// i.e. the values 100, 1000, 10000 are inserted at index-3.
```

### list.map and list.filter


```JSX
const l1 = [2, 3, 4]
l1.map(x => x + 10)
// Output would be [22, 23, 24]
```


```JSX
l1.map(x => (<div>{x + 2}</div>))
// Output would be [(<div>4</div>), (<div>5</div>), (<div>6</div>)]
```


```JSX
const l1 = [2, 3, 4, 5, 4]
l1.filter(x => (x != 4))
// Output would be [2, 3, 5]
```


```JSX
const l2 = [{id: 2, name: "A"}, {id: 5, name: "B"}]
l2.filter(x => x.id != 5)
// Output would be [{id: 2, name: "A"}]
```


```JSX
const l3 = [2, 3, 4, 5, 2, 5, 2, 5]
l1.filter(x => (x != 5))
// Output would be [2, 3, 4, 2, 2]
```

### Destructuring List


```JSX
// Old Way:

Const tmp = MyNameAndAge();
Const name = tmp[0];
Const age = tmp[1];

// new way

Const [name, age] = MyNameAndAge();

  const vehicles = ['mustang', 'f-150', 'expedition'];

const [car,, suv] = vehicles;
```

Learn more at w3schools -> React -> ES6 -> Destructuring


### Destructuring Dict

```JSX
function F() { return {a: 33, b: 44}; }

// Old way:
const tmp = F();
console.log(tmp.a, tmp.b);

// New way:
const {a, b} = F();
console.log(a, b);
```


### Shallow Copy / Deep Copy in JavaScript

Non-Atomic objects in JavaScript are actually referenced to the actual storage. If we assign a variable to some other variable, we are really copying the reference by default, not the value. To copy content of a list or dict, we must use spread-operator.

```JSX
a = [1, 2, 4];
b = a;
b.push(5);
```

Now, the value of `b` is  [1, 2, 4, 5] and the value of `a` is also `[1, 2, 4, 5]`, because `b` and `a` share the same reference. Which means the `b = a;` statement doesn’t copy the list.

```JSX
a = [1, 2, 4]
b = [...a]
b.push(5)
```

Now the value of `b` is `[1, 2, 4, 5]` but the value of `a` is still `[1, 2, 4]` because `a` and `b` are not sharing the same reference.

Which means `b = [...a]` is copying the content of `a` into a new list and assigning that new list to `b`.
As a result, when `5` is inserted into `b`, the content of `a` doesn’t change. This is called shallow-copying.

What is deep-copy - This is generally not used in JS and not encouraged because of performance overhead.

### concat list (add two lists)

```JSX
const list1 = [1, 2, 3]
const list2 = [10, 20, 30]
const new_list = [...list1, ...list2]
// Output of new_list would be [1, 2, 3, 10, 20, 30]
```

### Append / Add an item to a list

```JSX
const list1 = [1, 2, 3]
const new_list = [...list1, 10]
// Output of new_list would be [1, 2, 3, 10]
```

```JSX
const list1 = [{a: 1}, {a: 2}, {a: 3}]
const new_list = [...list1, {a: 10}]
// Output of new_list would be [{a: 1}, {a: 2}, {a: 3}, {a: 10}]

const x = {a: 100}
const new_list2 = [...list1, x]
// Output of new_list2 would be [{a: 1}, {a: 2}, {a: 3}, {a: 100}]

const y = 1000
const new_list3 = [...list1, y]
// Output of new_list3 would be [{a: 1}, {a: 2}, {a: 3}, 1000]
```

Prepend an item to a list:

i.e. Add an item at the starting of the list:

```JSX
const list1 = [1, 2, 3]
const new_list = [10, ...list1]
// Output of new_list would be [10, 1, 2, 3]
```


## Try Simple React Code Here

[Try Simple React code here](https://tinytrashbin.github.io/react_and_angularjs_short_notes/try_it/index.html).

Simple JSX / JavaScript code can be tried out in browser console.

For trying out more complex stuff, it is better idea to install node.js and clone the [sample repo](https://github.com/tinytrashbin/react_app_with_flask_backend)
