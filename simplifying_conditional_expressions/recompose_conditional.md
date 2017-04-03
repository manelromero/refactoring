## Recompose Conditional
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
### Replace Ternary Assignment with "Or" Assignment
```ruby
parameters = params ? params : []
```
#### Next
```ruby
parameters = params || []
```
### Replace Conditional with Explicit Return
```ruby
def reward_points
  if days_rented > 2
    2
  else
    1
  end
end
```
#### Next
```ruby
def reward_points
  return 2 if days_rented > 2
  1
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
