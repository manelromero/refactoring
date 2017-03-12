## Replace Loop with Collection Closure Method
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
managers = []
employees.each do |e|
  managers << e if e.manager?
end
```
#### Next
```ruby
managers = employees.select {|e| e.manager?}
```
#### Second example
```ruby
offices = []
employees.each {|e| offices << e.office}
```
#### Next
```ruby
offices = employees.map {|e| e.office}
```
#### Third example
```ruby
managerOffices = []
employees.each do |e|
  managerOffices << e.office if e.manager?
end
```
#### Next
```ruby
managerOffices = employees.select {|e| e.manager?}.
  map {|e| e.office}
```
#### Fourth example
```ruby
total = 0
employees.each {|e| total += e.salary}
```
#### Next
```ruby
total = employees.inject(0) {|sum, e| sum + e.salary}
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
