## Introduce Named Parameter
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
class SearchCriteria
  attr_reader :author_id, :publisher_id, :isbn

  def initialize(author_id, publisher_id, isbn)
    @author_id = author_id
    @publisher_id = publisher_id
    @isbn = isbn
  end
end

criteria = SearchCriteria.new(5, 8, "0201485672")
```
#### Next
```ruby
class SearchCriteria
  def initialize(params)
    @author_id = params[:author_id]
    @publisher_id = params[:publisher_id]
    @isbn = params[:isbn]
  end
end

criteria = SearchCriteria.new(
  :author_id => 5, :publisher_id => 8, :isbn =>"0201485672")
```
#### Next
```ruby
module CustomInitializers
  def hash_initializer(*attribute_names)
    define_method(:initialize) do |*args|
      data = args.first || {}
      attribute_names.each do |attribute_name|
        instance_variable_set "@#{attribute_name}", data[attribute_name]
      end
    end
  end
end

Class.send :include, CustomInitializers

class SearchCriteria
  hash_initializer :author_id, :publisher_id, :isbn
end
```
#### Second example
```ruby
class Books
  def self.find(selector, conditions="", *joins)
    sql = ["SELECT * FROM books"]

    joins.each do |join_table|
      sql << "LEFT OUTER JOIN #{join_table} ON"
      sql << "books.#{join_table.to_s.chap}_id"
      sql << " = #{join_table}.id"
    end

    sql << "WHERE #{conditions}" unless conditions.empty?
    sql << "LIMIT 1" if selector == :first

    connection.find(sql.join(" "))
  end
end

Books.find(:all)
Books.find(:all, "title like '%Voodoo Economics'")
Books.find(:all, "authors.name = 'Jenny James'", :authors)
Books.find(:first, "authors.name = 'Jenny James'", :authors)
```
#### Next
```ruby
module AssertValidKeys
  def assert_valid_keys(*valid_keys)
    unknown_keys = keys - [valid_keys].flatten
    if unknown_keys.any?
      raise(ArgumentError, "Unknown key(s): #{unknown_keys.join(", ")}")
    end
  end
end

Hash.send(:include, AssertValidKeys)

class Books
  def self.find(selector, hash={})
    hash.assert_valid_keys :conditions, :joins

    hash[:joins] ||= []
    hash[:conditions] ||= ""

    sql = ["SELECT * FROM books"]
    hash[:joins].each do |join_table|
      sql << "LEFT OUTER JOIN #{join_table}"
      sql << "ON books.#{join_table.to_s.chop}_id = #{join_table}.id"
    end

    sql << "WHERE #{hash[:conditions]}" unless hash[:conditions].empty?
    sql << "LIMIT 1" if selector == :first

    connection.find(sql.join(" "))
  end
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
