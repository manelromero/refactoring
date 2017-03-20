## Remove Unused Default Parameter
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
```ruby
def product_count_items(search_criteria = nil)
  criteria = search_criteria | @search_criteria
  ProductCountItem.find_all_by_criteria(criteria)
end
```
#### Next
```ruby
def product_count_items(search_criteria)
  ProductCountItem.find_all_by_criteria(search_criteria)
end
```
[back](https://github.com/manelromero/refactoring/blob/master/README.md)
