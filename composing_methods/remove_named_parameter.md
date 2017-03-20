## Remove Named Parameter
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
Books.find
Books.find(:selector => :all,
  :conditions => "authors.name = 'Jenny James'",
  :joins => [:authors])
Books.find(:selector => :first,
  :conditions => "authors.name = 'JennyJames'",
  :joins => [:authors])

class Books
  def self.find(hash={})
    hash[:joins] ||= []
    hash[:conditions] ||= ""

    sql = ["SELECT * FROM books"]
    hash[:joins].each do |join_table|
      sql << "LEFT OUTER JOIN #{join_table}"
      sql << "ON books.#{join_table.to_s.chop}_id = #{join_table}.id"
    end

    sql << "WHERE #{hash[:conditions]}" unless hash[:conditions].empty?
    sql << "LIMIT 1" if hash[:selector] == :first

    connection.find(sql.join(" "))
  end
end
```
#### Next
```ruby
class Books
  def self.find(selector, hash={})
    hash[:joins] ||= []
    hash[:conditions] ||= ""

    sql = ["SELECT * FROM books"]
    hash[:joins].each do |join_table|
      sql << "LEFT OUTER JOIN #{join_table} ON"
      sql << "books.#{join_table.to_s.chop}_id = #{join_table}.id"
    end

    sql << "WHERE #{hash[:conditions]}" unless hash[:conditions].empty?
    sql << "LIMIT 1" if selector == :first

    connection.find(sql.join(" "))
  end
end

Books.find(:all)
Books.find(:all, :conditions => "authors.name = 'Jenny James'",
  :joins =>[:authors])
Books.find(:first, :conditions => "authors.name = 'Jenny James'",
  :joins =>[:authors])
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
