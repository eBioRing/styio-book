# if...else

#### Basic

```
// if -> then
? (`expr`) -> {
    ...
}

// else
? !(`expr`) -> {
    ...
}
```

#### Simplify

```
? (`expr`) :) {
    ...
} :( {
    ... 
}
```

{% tabs %}
{% tab title="Java" %}
```java
if (`expr`) {
    // code block
} else {
    // code block
}
```
{% endtab %}

{% tab title="Python" %}
```python
if `expr`:
    ...
else:
    ...
```
{% endtab %}
{% endtabs %}

### Ternary Operator

```
(`expr`) ? `then` : `else`
```
