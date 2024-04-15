
## Structure:

```html
<Fater>
	<Child1/>
</Father>

**Child1:**
<Child1>
	<Child2/>
</Child1>
```

## Share information between components with no direct relationship

_Father to child of the child_

### Prop Drilling:

```html
<Father> -> *sharedProp*
	<Child1 sharedProp={sharedProp}/>
</Father>

**Child1:**
<Child1 sharedProp={sharedProp}>
	<Child2 sharedProp={sharedProp}/>
</Child1>
```

### Problems:

-   High coupling
-   Difficult to maintain
-   Difficult to understand

## State management with context:

```html
<Context.provider>
	<Father>
		<Child1/>
	</Father>
</Context.provider>

**Child1:**
<Child1>
	<Child2/>
</Child1>

Father modifies Context state and Child2 consumes it

*Father -> Context State -> Child2*
```

### Advantages:

-   Understandable
-   Scalable
-   Straight Forward

### Disadvantages :

-   Depends on the Context provider’s placement

```html
<Context.provider>
	<Father>
		<Child1/>
	</Father>
</Context.provider>

**Child1:**
<Child1>
	<Child2/>
</Child1>

<FatherOutsideContextProvider>
	<Child2/> -> *can't access context state*
</FatherOutsideContextProvider>
```

## Composition for the win

```html

<Father> -> *sharedProp*
	<Child1>
		<Child2 sharedProp={sharedProp}/>
	</Child1>
</Father>

**Child1:**
<Child1>
	{children}
</Child1>
```

### Advantages:

-   Easy
-   Scalable
-   No Dependencies
-   Reusable Code
-   Individual Logic

---

_So that’s all ! I hope this helps your code and project in a future, thanks for reading !_

_I want also to invite you to my Front End Community over [Discord](https://discord.gg/KEavKkDc5Y) ! where I do mentoring and give classes trough my [YouTube](https://www.youtube.com/watch?v=2jfIfeY4lrQ&t=1006s&ab_channel=GentlemanProgramming) channel._

_Happy coding everyone !!_