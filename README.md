drill_sergeant
==============

A potential gem to make lightweight unit tests easier to write in RSpec


## Examples
old way:
```ruby
describe MyClass do
  let(:some_instance_var) { FactoryGirl.create(:my_class) }
  
  it 'shoiuld return the expected output' do
    some_instance_var.method_1('foo', 'bar').should == 'baz'
    some_instance_var.method_1('foo', 'baz').should == 'bar'
    some_instance_var.method_1('bar', 'baz').should == 'foo'
    some_instance_var.method_1('foo', 'bar', 'baz').should == ''
  end
end
```
with Drill Sergeant:
```ruby
describe MyClass do
  let(:some_instance_var) { FactoryGirl.create(:my_class) }
  
  drill some_instance_var, :method_1 do
    with { ['foo', 'bar'] }.expect { 'baz' }
    with { ['foo', 'baz'] }.expect('bar')
    with('bar', 'baz').expect { 'foo' }
    with('foo', 'bar', 'baz').expect('')
  end
end
```
