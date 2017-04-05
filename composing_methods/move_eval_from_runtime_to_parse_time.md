## Move Eval from Runtime to Parse Time
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
class Person
  def self.attr_with_default(options)
    options.each_pair do |attribute, default_value|
      define_method attribute do
        eval "@#{attribute} ||= #{default_value}"
      end
    end
  end
  attr_with_default :emails => "[]",
                    :employee_number =>"EmployeeNumberGenerator.next"
end
```
#### Next
```ruby
class Person
  def self.attr_with_default(options)
    options.each_pair do |attribute, default_value|
      eval "define_method #{attribute} do
        @#{attribute} ||= #{default_value}
        end"
      end
    end

  attr_with_default :emails => "[]",
                    :employee_number =>"EmployeeNumberGenerator.next"
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
