drill_sergeant
==============

A small gem to make lightweight unit tests easier to write in RSpec


## Examples
```ruby
describe MyClass do
  let(:some_instance_var) { FactoryGirl.create(:my_class) }
  
  drill some_instance_var do
    target :method_1 do
      with { ['foo', 'bar'] }.expect { 'baz' }
      with { ['foo', 'baz'] }.expect('bar')
      with('bar', 'baz').expect { 'foo' }
      with('foo', 'bar', 'baz').expect('')
    end
  end
end
```
