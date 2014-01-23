drill_sergeant
==============

A potential gem to make lightweight unit tests easier to write in RSpec

Spawned from the idea of wanting to do something like:
```ruby
test_this = {
   MyModule::MyClass => {
       method_1: [
           { args: ['foo', 'bar'], expect: 'baz' },
           { args: ['foo', 'baz'], expect: 'bar' },
           { args: ['bar', 'baz'], expect: 'foo' },
       ]

   }
}
```


## Examples
old way:
```ruby
describe MyModule::MyClass do
  let(:some_instance_var) { FactoryGirl.create(:my_class) }
  
  it 'should return the expected output' do
    some_instance_var.method_1('foo', 'bar').should == 'baz'
    some_instance_var.method_1('foo', 'baz').should == 'bar'
    some_instance_var.method_1('bar', 'baz').should == 'foo'
    some_instance_var.method_1('foo', 'bar', 'baz').should == ''
    expect { some_instance_var.method_1('not_foo') }.to raise_error(SomeError)
  end
end
```
with Drill Sergeant:
```ruby
describe MyModule::MyClass do
  let(:some_instance_var) { FactoryGirl.create(:my_class) }
  
  drill some_instance_var, :method_1 do
    with { ['foo', 'bar'] }.expect { 'baz' }
    with { ['foo', 'baz'] }.expect('bar')
    with('bar', 'baz').expect { 'foo' }
    with('foo', 'bar', 'baz').expect('')
    with('not_foo').expect_error(SomeError)
  end
end
```
