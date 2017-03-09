## Introduce Explaining Variable
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
if (platform.upcase.index("MAC") &&
  browser.upcase.index("IE") &&
  initialized? &&
  resize > 0
  )
  # do something
end
```
#### Next
```ruby
is_mac_os = platform.upcase.index("MAC")
is_ie_browser = browser.upcase.index("IE")
was_resized = resize > 0

if (is_mac_os && is_ie_browser && initialized? && was_resized)
  # do something
end
```
### Second example
```ruby
def price
  # price is base price - quantity discount + shipping
  return @quantity * @item_price -
    [0, @quantity - 500].max * @item_price * 0.05 +
    [@quantity * @item_price * 0.1, 100.0].min
end
```
#### Next
```ruby
def price
  # price is base price - quantity discount + shipping
  base_price = @quantity * @item_price
  return base_price -
    [0, @quantity - 500].max * @item_price * 0.05 +
    [@quantity * @item_price * 0.1, 100.0].min
end
```
#### Next
```ruby
def price
  # price is base price - quantity discount + shipping
  base_price = @quantity * @item_price
  return base_price -
    [0, @quantity - 500].max * @item_price * 0.05 +
    [base_price * 0.1, 100.0].min
end
```
#### Next
```ruby
def price
  # price is base price - quantity discount + shipping
  base_price = @quantity * @item_price
  quantity_discount = [0, @quantity - 500].max * @item_price * 0.05
  return base_price -
    quantity_discount +
    [base_price * 0.1, 100.0].min
end
```
#### Next
```ruby
def price
  base_price = @quantity * @item_price
  quantity_discount = [0, @quantity - 500].max * @item_price * 0.05
  shipping = [base_price * 0.1, 100.0].min
  return base_price - quantity_discount + shipping
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
