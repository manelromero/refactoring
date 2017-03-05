## Inline Method
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
#### Initial
```ruby
def get_rating
  more_than_five_late_deliveries ? 2 : 1
end

def more_than_five_late_deliveries
  @number_of_late_deliveries > 5
end
```
#### Next
```ruby
def get_rating
  @number_of_late_deliveries > 5 ? 2 : 1
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
