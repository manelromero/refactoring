## Dynamic Method Definition
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
def failure
  self.state = :failure
end

def error
  self.state = :error
end

def success
  self.state = :success
end
```
#### Next
```ruby
[:failure, :error, :success].each do |method|
  define_method method do
    self.state = method
  end
end
```
#### Next
```ruby
class Class
  def def_each(*method_names, &block)
    method_names.each do |method_name|
      define_method method_name do
        instance_exec method_name, &block
      end
    end
  end
end

def_each :failure, :error, :success do |method_name|
  self.state = method_name
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
