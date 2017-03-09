## Replace Temp With Query
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
base_price = @quantity * @item_price
if (base_price > 1000)
  base_price * 0.95
else
  base_price * 0.98
end
```
#### Next
```ruby
if (base_price > 1000)
  base_price * 0.95
else
  base_price * 0.98
end

def base_price
  @quantity * @item_price
end
```
### Second example
```ruby
def price
  base_price = @quantity * @item_price
  if base_price > 1000
    discount_factor = 0.95
  else
    discount_factor = 0.98
  end
  base_price * discount_factor
end
```
#### Next
```ruby
def price
  a_base_price = base_price
  if a_base_price > 1000
    discount_factor = 0.95
  else
    discount_factor = 0.98
  end
  a_base_price * discount_factor
end

def base_price
  @quantity * @item_price
end
```
#### Next
```ruby
def price
  a_base_price = base_price
  if base_price > 1000
    discount_factor = 0.95
  else
    discount_factor = 0.98
  end
  a_base_price * discount_factor
end

def base_price
  @quantity * @item_price
end
```
#### Next
```ruby
def price
  if base_price > 1000
    discount_factor = 0.95
  else
    discount_factor = 0.98
  end
  base_price * discount_factor
end

def base_price
  @quantity * @item_price
end
```
#### Next
```ruby
def price
  a_discount_factor = discount_factor
  base_price * a_discount_factor
end

def base_price
  @quantity * @item_price
end

def discount_factor
  base_price > 1000 ? 0.95 : 0.98
end
```
#### Next
```ruby
def price
  base_price * discount_factor
end

def base_price
  @quantity * @item_price
end

def discount_factor
  base_price > 1000 ? 0.95 : 0.98
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
