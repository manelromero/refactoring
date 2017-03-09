## Replace Method with Method Object
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
class Account
  def gamma(input_val, quantity, year_to_date)
    inportant_value1 = (input_val * quantity) + delta
    important_value2 = (input_val * year_to_date) + 100
    if (year_to_date - important_value1) > 100
      important_value2 -= 20
    end
    important_value3 = important_value2 * 7
    # and so on.
    important_value3 - 2 * important_value1
  end
end
```
#### Next
```ruby
class Gamma
  attr_reader :account,
              :input_val,
              :quantity,
              :year_to_date,
              :important_value1,
              :important_value2,
              :important_value3
  end

  def initialize(account, input_val_arg, quantity_arg, year_to_date_arg)
    @account = account
    @input_val = input_val_arg
    @quantity = quantity_arg
    @year_to_date = year_to_date_arg
  end

  def compute
    @inportant_value1 = (input_val * quantity) + @account.delta
    @important_value2 = (input_val * year_to_date) + 100
    if (year_to_date - important_value1) > 100
      @important_value2 -= 20
    end
    @important_value3 = important_value2 * 7
    # and so on.
    @important_value3 - 2 * important_value1
  end

def gamma(input_val, quantity, year_to_date)
  Gamma.new(self, input_val, quantity, year_to_date).compute
end
```
#### Next
```ruby
def compute
  @inportant_value1 = (input_val * quantity) + @account.delta
  @important_value2 = (input_val * year_to_date) + 100
  important_thing
  @important_value3 = important_value2 * 7
  # and so on.
  @important_value3 - 2 * important_value1
end

def important_thing
  if (year_to_date - important_value1) > 100
    @important_value2 -= 20
  end
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
