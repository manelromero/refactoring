## Remove Assignments to Parameters
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
def discount(input_val, quantity, year_to_date)
  if input_val > 50
    input_val -= 2
  end
end
```
#### Next
```ruby
def discount(input_val, quantity, year_to_date)
  result = input_val
  if input_val > 50
    result -= 2
  end
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
