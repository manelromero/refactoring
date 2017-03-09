## Extract Method
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
### No local variables
#### Initial
```ruby
def print_owing
  outstanding = 0.0

  # print banner
  puts "*************************"
  puts "***** Customer Owes *****"
  puts "*************************"

  # calculate outstanding
  @orders.each do |order|
    outstanding += order.amount
  end

  # print details
  puts "name: #{@name}"
  puts "amount: #{outstanding}"
end
```
#### Next
```ruby
def print_owing
  outstanding = 0.0

  print_banner

  # calculate outstanding
  @orders.each do |order|
    outstanding += order.amount
  end

  # print details
  puts "name: #{@name}"
  puts "amount: #{outstanding}"
end

def print_banner
  puts "*************************"
  puts "***** Customer Owes *****"
  puts "*************************"
end
```
### Using local variables
```ruby
def print_owing
  outstanding = 0.0

  print_banner

  # calculate outstanding
  @orders.each do |order|
    outstanding += order.amount
  end

  print_details outstanding
end

def print_banner
  puts "*************************"
  puts "***** Customer Owes *****"
  puts "*************************"
end

def print_details(outstanding)
  puts "name: #{@name}"
  puts "amount: #{outstanding}"
end
```
### Reassigning a local variable
```ruby
def print_owing
  print_banner
  outstanding = calculate_outstanding
  print_details outstanding
end

def print_banner
  puts "*************************"
  puts "***** Customer Owes *****"
  puts "*************************"
end

def calculate_outstanding
  outstanding = 0.0
  @orders.each do |order|
    outstanding += order.amount
  end
  outstanding
end

def print_details(outstanding)
  puts "name: #{@name}"
  puts "amount: #{outstanding}"
end
```
#### Next
```ruby
def print_owing
  print_banner
  outstanding = calculate_outstanding
  print_details outstanding
end

def print_banner
  puts "*************************"
  puts "***** Customer Owes *****"
  puts "*************************"
end

def calculate_outstanding
  @orders.inject(0.0) { |result, order| result + order.amount }
end

def print_details(outstanding)
  puts "name: #{@name}"
  puts "amount: #{outstanding}"
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
