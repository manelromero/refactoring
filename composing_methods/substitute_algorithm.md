## Substitute Algorithm
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
def found_friends(people)
  friends = []
  people.each do |person|
    if(person == "Don")
      friends << "Don"
    end
    if(person == "John")
      friends << "John"
    end
    if(person == "Kent")
      friends << "Kent"
end end
  return friends
end
```
#### Next
```ruby
def found_friends(people)
  people.select do |person|
    %w(Don John Kent).include? person
  end
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
