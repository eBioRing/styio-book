# Syntax Overview

## Hello, World!

```
>_("Hello, Styio!")
```

## Basic Type

#### Boolean

```
x = $T

x = $F
```

#### Integer

```
x : i32 = 0
```

#### Float

```
y : f64 = 0.0
```

#### Char

```
z = '\n'
```

## Project

#### Import Module

```
@(
  "module"
) -> {
  
}
```

## Resource

#### Resource Declaration (Global) (Can Only Be Assigned Once)

```
@(x, y)
```

#### Resource Assignment (Immutable) (Final)

```
@(x) <- "data.csv"
```

#### Resource Definition (Immutable) (Final)

```
@(x <- "data.csv")
```

## Variable

#### Variable Declaration (Global) (Mutable) (Flexible)

```
x: i32
```

#### Variable Definition (Global) (Mutable) (Flexible)

```
x: f64 = 0.3
```

#### Variable Assignment (Global) (Mutable) (Flexible)

```
x = 0
```

#### Variable Assignment (Global) (Immutable) (Final)

```
x := 0
```

## Function

#### Function Declaration (Accept Overload) (Flexible) (Danger!)

```
# f = (x) => {
  == x ==>
}

# f = (x, y) => {
  == x + y ==>
}
```

#### Function Definition (Reject Overload) (Final)

```
# f := (x, y) => {
  == x + y ==>
}
```

#### Function Declaration / Definition (With Optional Arguments)

```
# f = (x, *) => {

}

# f := (x, *) => {

}
```

#### Function Declaration / Definition (With Optional Arguments and Keyword Arguments)

```
# f = (x, *, **) => {

}

# f := (x, *, **) => {

}
```

#### Closure / Anonymous Function / Lambda Expression

```
#(x, y) => {
  == x + y ==>
}
```

## Enumeration

#### Definition (Final)

```
# Type := {
  | Some,
  | None,
}
```

## Struct

#### Struct Definition (Reject Overload) (Final)

```
# Point := (
  x: f64, 
  y: f64,
)
```

#### Struct: Inherit

```
# Point3D 
  <: {
    Point; 
    Else;
  } 
  := (
    x: f64,
    y: f64,
    z: f64,
  )
```

#### Struct: Extra Methods

```
# Point := (
  x: f64, 
  y: f64,
) +: {
  eval := () => {
    == (x, y) ==
  }
}
```

### Evaluation

```
$ sum 
  = {
    result <- 0;
  }
  >> (
    x
  ) 
  => {
    result += x
  }
  -> result
```

```
$ count 
  = {
    result <- 0;
  }
  >> (
    x
  )
  => {
    result += 1
  }
  -> result
```

```
$ [avg, mean]
  = {
    count <- 0;
    sum <- 0;
  }
  >> (
    x
  )
  => {
    count += 1
    sum += x
  } 
  -> (sum, count) 
  => {
    == sum / count ==>
  }
```

```
$ min
  = {
    result;
  }
  >> (
    x
  )
  => {
    ?? (result != {})
    :) {
      ?? (x < result)
      :) {
        result = x
      }
      :( {
        >>>>>>>>>>
      }
    }
    :( {
      result = x
    }
  } 
  -> result
```

```
$ max
  = {
    result;
  }
  >> (
    x
  )
  => {
    ?? (result != {})
    :) {
      ?? (x > result)
      :) {
        result = x
      }
      :( {
        >>>>>>>>>>
      }
    }
    :( {
      result = x
    }
  } 
  -> result
```

#### Use evaluation pipeline

```
max_val = array |> ${max}
```

#### Extra: Evaluate Stream Computing

```
$ sum_revenue
  = {result}
  >> (x) 
  => {
    result += x.revenue
  }
  -> result
```

#### Extra: Stream Template

```
$ extract_fields
  >> (k, v)
  ~> (k.name, k.age)
```

```
$ sum_revenue
  >> (k, v)
  ~> {
    k.uuid,
    count(k.region),
    sum(k.price),
  }
```

## Collection

### String

```
"Hello, Styio!"
```

```
'Hello, Styio!'
```

#### Format String

```
name = "Styio"

"Hello, {name}!"
```

```
name = 'Styio'

'Hello, {name}!'
```

#### Verbatim String (Resource)

```
@"Hello, World!"
```

```
@'Hello, World!'
```

#### Raw String

```
"""
Why do you need this?
"""
```

```
'''
Why do you need this?
'''
```

### Tuple

```
(0, 1, 2)
```

### Array

```
x: i32[100] = [0..]
```

### List

```
[1, 2, 3, 4, 5, 6]
```

#### Get size (length) of the list

<pre><code>list = [1, 2, 3, 4, 5, 6]

|list|

<strong>&#x3C;/> 6
</strong></code></pre>

#### Push / Append / Add an element to the tail

<pre><code>list = [1, 2, 3, 4, 5, 6]

list ]&#x3C; 7

<strong>&#x3C;/> [1, 2, 3, 4, 5, 6, 7]
</strong></code></pre>

#### Pop / Delete the last element

<pre><code>list = [1, 2, 3, 4, 5, 6]

item = list ]>

<strong>&#x3C;/> [1, 2, 3, 4, 5]
</strong></code></pre>

#### Reversed

<pre><code>list[&#x3C;]

<strong>&#x3C;/> [6, 5, 4, 3, 2, 1]
</strong></code></pre>

#### Get an element by index

<pre><code>list = ['a', 'b', 'c']

list[0]

<strong>&#x3C;/> a
</strong></code></pre>

#### Get index of an element

<pre><code>list = ['a', 'b', 'c']

list[?= 'b']

<strong>&#x3C;/> 1
</strong></code></pre>

#### Insert an element by index

<pre><code>list = ['a', 'b', 'd']

list[+: 2 &#x3C;- 'c']

<strong>&#x3C;/> ['a', 'b', 'c', 'd']
</strong></code></pre>

#### Insert an element to the head

<pre><code>list = ['b', 'c', 'd']

list[+: 0 &#x3C;- 'a']

<strong>&#x3C;/> ['a', 'b', 'c', 'd']
</strong></code></pre>

#### Remove an element by index

<pre><code>list = ['a', 'o', 'b', 'c']

list[-: 1]

<strong>&#x3C;/> ['a', 'b', 'c']
</strong></code></pre>

#### Remove elements by many indices

<pre><code>list = ['a', 'o', 'b', 'c']

list[-: (1, 2)]

<strong>&#x3C;/> ['a', 'b', 'c']
</strong></code></pre>

#### Remove an element by value (from left to right)

<pre><code>list = [1, 2, 3]

list[-: ?= 2]

<strong>&#x3C;/> [1, 3]
</strong></code></pre>

#### Remove elements by many values (from left to right)

<pre><code>list = [1, 2, 3]

list[-: ?^ (2, 3)]

<strong>&#x3C;/> [1]
</strong></code></pre>

#### Remove element by value (from right to left)

```
list = [1, 2, 3, 2]

list[[<] -: ?= 2]

</> [1, 2, 3]
```

#### Remove elements by condition

<pre><code>list = [1, 2, 3]

list >> x -: ?(x &#x3C;= 2)

<strong>&#x3C;/> [3]
</strong></code></pre>

#### Add elements by lambda function (Danger!)

```
list = [(1, 3), (2, 4)]

list >> (x, y) +: {
    // This is a lambda function.
}
```

#### Remove elements by lambda function (Danger!)

```
list = [(1, 3), (2, 4)]

list >> (x, y) -: {
    // This is a lambda function.    
}
```

#### Form a list from another list

```
a = [] << {
  b >> x => {
    == x ==>
  }
}
```

#### Form a list from a dictionary

```
a = [] << {
  d >> (k, v) => {
    == v ==>
  }
}
```

### Record

```
< name = "Alice", 
  age = 15,
>
```

#### Get the value by name of attribute (item)

```
record.name
```

```
record['name']
```

### Dictionary

```
{
  "A": "Alice",
  "B": "Bob",
}
```

#### Get value by key

```
dict["C"]
```

#### Add Key-Value Pair

```
dict["C"] = "Clare"
```

#### Remove key-value pair

```
dict[-: "B"]
```

#### Update dictionary by another dictionary

```
d1 <- d2
```

#### Decompose

```
d ~ (k, v)
```

#### Get keys

```
// As a list (value expression)
[d ~ (k, v) -> k]

// As a variable (still a list)
k <- [d ~ (k, v)]
```

#### Get values

```
// As a list (value expression)
[d ~ (k, v) -> v]

// As a variable (still a list)
v <- [d ~ (k, v)]
```

#### Apply Lambda Function

```
dict >> (x, y) => {
    
}
```

## Control Flow

### Condition / Cases

#### if ... then ... else ...

```
?( /* Condition */ ) 
:) {
    
} 
:( {

}
```

#### match

```
val ?= {
  0 => {
    // Do Something
  } 
  
  1 => {
    // Do Something
  }
  
  _ => {
    // Do Something
  }
}
```

## Loop / Iteration

#### Before We Start, You Need To Know:

#### Return

```
== x ==>
```

#### Break

```
^^^^^^^^
```

#### Continue

```
>>>>>>>>
```

### Infinite Loop

```
[...] >> {

}
```

#### Infinite Loop (With Auto Cast + Match Cases)

{% code title="Match Cases (Only One)" %}
```
x = 1

[...] >> x ?= 1 => {
  >_("x is 1")
}
```
{% endcode %}

{% code title="Match Cases (Many)" %}
```
x = 0
c = 0

[...] >> x ?= {
  0 => {
    x = 1
    
    ?(c >= 10) 
    :) {
      ^^^^^^^^
    }
  }
  
  1 => {
    x = 0
    c = c + 1
  }
  
  _ => {
    !!! <- "You should not reach this line, and there must be something wrong."
  }
}
```
{% endcode %}

### Range

#### Range Iterator

```
[0..10] >> {
  
}
```

#### Range Iterator (With Auto Cast)

```
[0..10] >> x => {
  >_(x)
}
```

#### Range Iterator (With Auto Cast + Match Cases)

{% code title="Match Cases (Only One)" %}
```
[0..10] >> (x) ?= 5 => {
  >_("x is 5")
}
```
{% endcode %}

{% code title="Match Cases (Branches)" %}
```
[0..10] >> (x) ?= {
  0 => { >_("x is 0") }
  1 => { >_("x is 1") }
  _ => { >_("Default") }
}
```
{% endcode %}

#### Range Iterator (With Auto Cast + Check Is In)

```
[0..10] >> (x) ?^ (2, 3, 5, 7) => {
  >_("x is prime number")
}
```

#### Range Iterator (With Auto Cast + Check Condition)

```
[0..10] >> (x) ? (x % 2 == 0) :) {
  >_("x is even number")
}
```

### List

#### List Iterator

```
[0, 1, 2] >> {
    
}
```

#### List Iterator (With Auto Cast)

```
[0, 1, 2] >> x => {
    >_("x")
}
```

#### List Iterator (With Auto Cast + Match Cases)

{% code title="Match Cases (Only One)" %}
```
[0, 1, 2] >> (x) ?= 0 => {
  >_("x is 0")
}
```
{% endcode %}

{% code title="Match Cases (Branches)" %}
```
[0, 1, 2, 3, 4] >> x ?= {
  0 => { >_("x is 0") }
  1 => { >_("x is 1") }
  _ => { >_("Default") }
}
```
{% endcode %}

#### List Iterator (With Auto Cast + Check Is In)

```
[0, 1, 2, 3, 4, 5] >> (x) ?^ (2, 3, 5) => {
  >_("x is prime number")
}
```

#### List Iterator (With Auto Cast + Check Condition)

```
[0, 1, 2] >> (x) ? (x % 2 == 1) :) {
  >_("x is odd number")
}
```

## IO

#### Print

```
>_("Styio!")
```

#### Read File

```
x <- @("data.csv")
```

#### Write File

```
x -> @("data.csv")
```

#### Download From Link

```
x <- @("https://some.link/path/to/file.json")
```

#### Listen Web Socket (Block Thread)

```
@("localhost:35752") >> {
    
}
```

## Concurrent

```
{
& =>
& =>
& =>
}
```

```
{
% => 
% => 
% =>
}
```

### Lock (I'm sure there is a way but just can't find now.)

```
*|>

<|*
```

## Exception handling

```
!!! <- "Error: There is something wrong."
```

### Operator Overload

```
# This : {

}
  +: {
  `$? + {Other}`: {}
}
```

<table><thead><tr><th width="309">Template (Format Expression)</th><th>Description</th></tr></thead><tbody><tr><td><pre><code>`- $?` : {}
</code></pre></td><td>Negative: <code>- This</code></td></tr><tr><td><pre><code>`$? + {Other}` : {}
</code></pre></td><td>Binary Addition: <code>This + Other</code></td></tr><tr><td><pre><code>`$? - {Other}` : {}
</code></pre></td><td>Binary Subtraction: <code>This - Other</code></td></tr><tr><td><pre><code>`$? * {Other}` : {}
</code></pre></td><td>Binary Multiplication: <code>This * Other</code></td></tr><tr><td><pre><code>`$? / {Other}` : {}
</code></pre></td><td>Binary Division: <code>This / Other</code></td></tr><tr><td><pre><code>`$? ** {Other}` : {}
</code></pre></td><td>Math: Power {Base: <code>This</code>, Exponent: <code>Other</code>}</td></tr><tr><td><pre><code>`$? % {Other}` : {}
</code></pre></td><td>Math: Modulo {Dividend: <code>This</code>, Divisor: <code>Other</code>}</td></tr><tr><td><pre><code>`{Other} + $?` : {}
</code></pre></td><td>Reversed Addition: <code>Other + This</code></td></tr><tr><td><pre><code>`{Other} - $?` : {}
</code></pre></td><td>Reversed Addition: <code>Other - This</code></td></tr><tr><td><pre><code>`{Other} * $?` : {}
</code></pre></td><td>Reversed Addition: <code>Other * This</code></td></tr><tr><td><pre><code>`{Other} / $?` : {}
</code></pre></td><td>Reversed Addition: <code>Other / This</code></td></tr><tr><td><pre><code>`{Other} ** $?` : {}
</code></pre></td><td>Math: Power {Base: <code>Other</code>, Exponent: <code>This</code>}</td></tr><tr><td><pre><code>`{Other} % $?` : {}
</code></pre></td><td>Math: Modulo {Dividend: <code>Other</code>, Divisor: <code>This</code>}</td></tr><tr><td><pre><code>`$? += {Other}` : {}
</code></pre></td><td><code>Other += This</code></td></tr><tr><td><pre><code>`$? -= {Other}` : {}
</code></pre></td><td><code>Other -= This</code></td></tr><tr><td><pre><code>`$? *= {Other}` : {}
</code></pre></td><td><code>Other *= This</code></td></tr><tr><td><pre><code>`$? /= {Other}` : {}
</code></pre></td><td><code>Other /= This</code></td></tr><tr><td><pre><code>`$? %= {Other}` : {}
</code></pre></td><td><code>Other %= This</code></td></tr><tr><td><pre><code>`! $?` : {}
</code></pre></td><td>Logic NOT: <code>! This</code></td></tr><tr><td><pre><code>`$? &#x26;&#x26; {Other}` : {}
</code></pre></td><td>Logic AND: <code>This &#x26;&#x26; Other</code></td></tr><tr><td><pre><code>`$? || {Other}` : {}
</code></pre></td><td>Logic OR: <code>This || Other</code></td></tr><tr><td><pre><code>`$? ^ {Other}` : {}
</code></pre></td><td>Logic XOR: <code>This || Other</code></td></tr><tr><td><pre><code>`$? &#x26; {Other}` : {}
</code></pre></td><td>Bit AND: <code>This &#x26; Other</code></td></tr><tr><td><pre><code>`$? | {Other}` : {}
</code></pre></td><td>Bit OR: <code>This | Other</code></td></tr><tr><td><pre><code>`$? >> {Other}` : {}
</code></pre></td><td>Bit Right Shift: <code>This >> Other</code></td></tr><tr><td><pre><code>`$? &#x3C;&#x3C; {Other}` : {}
</code></pre></td><td>Bit Left Shift: <code>This &#x3C;&#x3C; Other</code></td></tr><tr><td><pre><code>` % |$?| ` : {}
</code></pre></td><td>Method: Get size (length) of <code>This</code></td></tr><tr><td><pre><code>` % "$?" ` : {}
</code></pre></td><td>Method: Get string of <code>This</code></td></tr><tr><td><pre><code>`% :&#x3C; $?` : {}
</code></pre></td><td>Method: Get type of <code>This</code></td></tr><tr><td><pre><code>`$?[{Item}]` : {}
</code></pre></td><td>Method: Get <code>Item</code> of <code>This</code></td></tr><tr><td><pre><code>`$?[{Item}] = {Value}` : {}
</code></pre></td><td>Method: Set <code>Item</code> of <code>This</code> as <code>Value</code></td></tr><tr><td><pre><code>`$?.{Attr}` : {}
</code></pre></td><td>Method: Get <code>Attr</code> of <code>This</code></td></tr><tr><td><pre><code>`$?.{Attr} = {Value}` : {}
</code></pre></td><td>Method: Set <code>Attr</code> of <code>This</code> as <code>Value</code></td></tr><tr><td><pre><code>`$?[&#x3C;]` : {}
</code></pre></td><td>Method: Get reversed collection.</td></tr><tr><td><pre><code>`$? ?^ {List}` : {}
</code></pre></td><td>Method: Check if <code>This</code> in <code>List</code> or not.</td></tr><tr><td><pre><code>`$? >>` : {}
</code></pre></td><td>Iterator: Implement an iterator for <code>This</code> collection.</td></tr><tr><td><pre><code>`$?()` : {}
</code></pre></td><td>Trigger: When an instance of <code>This</code> is called, do ...</td></tr><tr><td><pre><code>`$?(x, y)` : {}
</code></pre></td><td>Trigger: When an instance of <code>This</code> is called, with arguments of <code>(x, y)</code>, do ...</td></tr><tr><td><pre><code>`$?(*, **)` : {}
</code></pre></td><td>Trigger: When an instance of <code>This</code> is called, with optional arguments of <code>*</code>, and keyword arguments of <code>**</code>, do ...</td></tr></tbody></table>

