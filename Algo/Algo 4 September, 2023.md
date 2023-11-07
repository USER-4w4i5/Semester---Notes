### Algo characteristics

- Definiteness
	- Steps must be precisely define
- Effectiveness
	- Individual steps are all do able
- Finiteness
	- It should not take forever to produce an output for any given input
- Output
	- Info/Data that goes out
- Other Important Feature
	- Input
		- Info/Data that comes in
	- Correctness
		- Output relates correctly to inputs
	- Generality
		- Works for many possible inputs
	- Efficiency
		- Takes less time & memory to run

## Complexity Analysis

- **Platform Independence**
	- Ideal Algo
		- Each elementary operation takes 1 step of time
		- Each elementary instance occupies 1 unit of memory

#### Analyzing an Algo statements
- Order of O's
	- Goes in order of Best to Worst
		- O(1)
		- O(log(N))
		- O(N)
		- O(n\*log(n))
		- O(n^m), where m is any number > 0
		- O(2^n)
		- O(!n)
- Simple Statement 
	- Order of O(1)
	- Basic step = 1, as long as number of statements are constant
	- Examples
		- Assignments: `int x = y;`
		- Arithmetic Operations: `x += i;`
		- Array Referencing: `A\[j\] = 5;`
		- Conditionals (Most): `if(x<12){};`
- Simple Loop
	- Basic step = N x 1
	- Quiz Note:: For a reminder on how a for loop works
		- int i = 0. This is the starting point for the loop
		- i < n. This is a condition thats checked at the end of every iteration
		- i++.  
```
//Here even if the loop increments by N it will still be N times and therefore the complexity is O(n)
	for(int i =0; i < n; i++){
		s      //Statement that does stuff
	}

//However for factors i.e the iterator being multiplied or divided the time complexity is O(log(n))
	for(int i =0; i < n; i*n){
		s      //Statement that does stuff
	}

//For the iterator going up in order of power i.e from i^2 to i^3 or from i^2 to sqrt(i) the complexity is O(log(log(n)))
	for(int i =0; i < n; i=pow(i,c)){
		s      //Statement that does stuff
	}

> 2^(c^i) = n      //Take log of base 2 on both sides
> log2(2^(c^i)) = log2(n)
> c^i = log(n)     //Take log of base c on both sides
> logc(c^i) = logc(log(n)
> i = log(c(log(n)))
```

- Nested Loops
	- Basic step = i x j
	- Where i and j increment by one only
	- order of O(n2)
```
for(int i =0; i < n; i++){
	for(int j =0; j < n; j++){
		s      //Statement that does stuff
	}
}
```
- Inner Loop depends on Outer Loop
	- Where Outer loop goes till N and inner loop goes till outer loop index
		- Inner loop is executed N time while the outer loop is
	- Pick the highest order `This went over my head`
	- order of O(n2) thru n(n+1)/2
```
for(int i =0; i < n; i++){
	for(int j =0; j < i; j++){
		s      //Statement that does stuff
	}
}


```
- Array
	- Loop where a Sum of all elements is calculated
#### Analyzing Loops
- Already covered above, however for practice check out Lecture 2 page 12+ slides that maam uploaded

#### Analyzing sequence of statements
- Generally observe the time complexity of each statement line-by-line and sum it all up. 
	- The sum is the final answer with the coefficients and low order factors discarded
- If-Statements
	- These statements themselves are always o(1)
	- However, Big-Oh assumes the worst case/Upper limit therefore we pick whatever higher order value for O() we can get
