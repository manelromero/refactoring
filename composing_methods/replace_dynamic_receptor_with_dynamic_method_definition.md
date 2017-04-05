## Replace Dynamic Receptor with Dynamic Method Definition
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
class Person
  attr_accessor :name, :age
  def method_missing(sym, *args, &block)
    empty?(sym.to_s.sub(/^empty_/,"").chomp("?"))
  end

  def empty?(sym)
    self.send(sym).nil?
  end
end
```
#### Next
```ruby
class Person
  def self.attrs_with_empty_predicate(*args)
    attr_accessor *args
    args.each do |attribute|
      define_method "empty_#{attribute}?" do
        self.send(attribute).nil?
      end
    end
  end
  attrs_with_empty_predicate :name, :age

end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
