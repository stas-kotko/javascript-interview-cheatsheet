## Loops

```
while (cond) { … }

do { … } while (cond)

for (start; cond; step) { … }
```

`for` loop can use “inline” var declaration: `for (let i = 0 …`
This var is only visible inside the loop

`for` loop algorithm: 
- start – once per loop
- check the condition
- perform the code in the body
- perform step

`break` keyword exits from the loop immediately passing the control to the next line after the loop.

`continue` stops the current iteration and starts a new one if the condition allows it.

### Labels
```
label: for (...) {
	break label
	// or
	continue label
}
```
Labels are used for nested loops.

### Iteration methods difference
`Object.getOwnPropertynames(obj)` – returns non-symbol keys.  
`O.getOwnPropertySymbols(o)` – returns symbol keys only.  
`O.keys/values()` – non-symbol keys/values with enumerable flag.  
`for .. in` – loops over non-sym keys with enumerable flag, plus prototype’s keys.  

All of the use internal method [[OwnPropertyKeys]] to get a list of props (“ownKeys” trap in Proxy)
