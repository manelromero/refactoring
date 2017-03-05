# Inline Temp
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
#### Initial
```ruby
base_price = an_order.base_price
return (base_price > 1000)
```
#### Next
```ruby
return (an_order.base_price > 1000)
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
