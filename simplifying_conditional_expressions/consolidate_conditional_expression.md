## Consolidate Conditional Expression
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
def disability_amount
  return 0 if @seniority < 2
  return 0 if @months_disabled > 12
  return 0 if @is_part_time
  # compute the disability amount
  ...
```
#### Next
```ruby
def disability_amount
  return 0 if @seniority < 2 || @months_disabled > 12 || @is_part_time
  # compute the disability amount
  ...
```
#### Next
```ruby
def disability_amount
  return 0 if ineligable_for_disability?
  # compute the disability amount
  ...
end

def ineligible_for_disability?
  @seniority < 2 || @months_disabled > 12 || @is_part_time
end
```
#### Second example
```ruby
if on_vacation?
  if length_of_service > 10
    return 1
  end
end
0.5
```
#### Next
```ruby
if on_vacation? && length_of_service > 10
  return 1
end
0.5
```
#### Next
```ruby
return 1 if on_vacation? && length_of_service > 10
0.5
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
