# Input Boxes

![[Pasted image 20240621153118.png]]
![[Pasted image 20240621153151.png]]

# Buttons

![[Pasted image 20240621153309.png]]

# Checkboxes

![[Pasted image 20240622131526.png]]
![[Pasted image 20240621153421.png]]

# Angela

## Data Types

1) string
2) numbers
3) boolean

- prompt - allows for inputs otherwise, its the same as alert
- alert
- var - for variables
- .length()
- slicing [same way as python]
	- .slice(x,y)
- .toUpperCase()
- .toLowerCase()
- Math.random() = helps generate random numbers

## Comparators
- ===
	- is equal to
- !==
	- is not equal to
- >, <, >=, <=

Q) how is === different from == ?
A)  " === " checks if the data type is equal as well
" == " checks if the value is the same

```js
var a = 1
var b = '1'
```
a == b => true
a === b => false

# How it is used in DOM

- inline
- internal
- external

- getElementsByTagName
- getElementsByClassName
- getElementById
- querySelector
.add
.toggle
.innerHTML

.addEventListener
https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener
https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers
https://developer.mozilla.org/en-US/docs/Web/Events/Creating_and_triggering_events
https://developer.mozilla.org/en-US/docs/Web/API/Element/keypress_event

## Higher order function and Callback function

when u pass a function as a parameter and the parameter function is the callback function 

```js
function add(a, b){return a+b;}
function sub(a, b){return a-b;}
function mul(a, b){return a*b;}
function div(a, b){return a/b;}

function calculator(a, b, operator){
	return operator(a,b);
}

calculator(a,b,add); //here add is a callback function
calculator(a,b,sub);
calculator(a,b,mul);
calculator(a,b,div);
```

- objects and constructor functions - literally OOPS
- methods - basically class functions