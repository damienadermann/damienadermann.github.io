---
layout: post
title: "Death to Nil"
date: "2016-04-01 11:21:21 +1100"
---

How do we avoid the ever present **"Ruby error: undefined method 'something' for nil:NilClass"**? I have the golden answer

*Don't ever use nil!*

Its so simple. But like all simple ideas it needs a laborious explanation

As a software developer the most common error I find myself looking for in code reviews is nil chaos. Nil being such an innocent idea that has caused so many problems over the years for people worldwide.

As ruby developers we are given the flexibility of dynamic typing, so you'd think this freedom would keep us safe from nil. I'd like to make an argument, it does. Let me explain, ruby is flexible because we don't care what type is being excepted as an argument to a method or class. We just care that it fits a certain interface. So if we have the method

```ruby
def length(string)
  string.length
end
```

we don't care whether string is actually a string, we care that it responds to length.

```ruby
length("string") #6
length(%w(s t r i n g)) #6
```

So in ruby we don't care what type we are using, we care about the interface of the object we are using. Does this object [quack like a duck?](https://en.wikipedia.org/wiki/Duck_typing)?

But what if we pass nil to length

```ruby
length(nil) #Boom
```

It blows up. Of course it does. That code is dumb. So why do we always hit this simple issue? Its because we don't usually know what type a variable is, which in ruby we don't actually care about, but we do care what the interface is. We can find the length of an array or a string but not Nil because nil has a completely different interface.

So the trick is always pass around variables that have the same interface. This means all methods should return values with the same interface (nil is an interface too). Most of the time this is simple but Mr nil comes along and complicates this

So whats the interface?

```ruby
class Dog
  def initialize(name)

  end
  def name
    @name
  end
end

myPetDog = Dog.new('Maverick')
wildDog = Dog.new(nil)

length(myPetDog.name) #"Maverick"
length(wildDog.name) #Boom
```

The obvious fix to this is just don't create a Dog with no name but we don't always have control of this. So the problem becomes Dog#name can return a value with the interface of #name or an interface of no methods.

So in the example we can put the fire out

```
if wildDog.name
  length(wildDog.name)
end
```

or can just not set the fire in the first place by not letting name return nil, keeping the interface simple

```
def name
  @name || ''
end
```

This sounds too simple but this technique can be used in almost all situations, with slightly different implementations

Two common techniques help us do this is the [Null Object Pattern](https://robots.thoughtbot.com/rails-refactoring-example-introduce-null-object) and the [Optional Pattern](https://medium.com/learnings-in-and-around-sharetribe/option-pattern-in-ruby-7b0f7c5abdb6#.mzdo9ylld)

I won't go into the details on each of these (because you probably know more about them than me) but essentially they help us always return one interface from a method so that anything using the result of that method can expect only one interface.

I will make a little note on the optional pattern though. I love the optional pattern in typed languages but it feels unruby, which is probably why its not used much in ruby. All the optional pattern does is force you to check for nil before using a value. Ruby doesn't care about types and so if we know that the interface being passed to a method is nullable then we treat it as such.

```ruby
def method1(value)
  if value.is_some?
    value.get.do_something
  end
end
```

really does the same as

```ruby
def method2(value)
  unless value.nil?
    value.do_something
  end
end
```

method2 is safe and always expects the same interface, a nullable value which is the same as method1 which is safe because it always expects an optional value. Its the same thing.

I said "Don't ever use nil". And this holds true here. We aren't using nil. We are using an object with the interface that responds to #nil? and optionally responds to #do_something. And as long as this method responds with a consistent interface any object using this method won't hit a nil error either. This method always return nil so no one will ever try to call a method on it. Its a grey line and should be used as a last resort.

Anyway thats it. Don't use nil. I'll end with a few practical tips to help us return consistent interfaces instead of nil

- When using ActiveRecord always add a default to the db column
- Never return nil from a method that returns an enumerable, just return an empty set.
- Don't ever use `#try` or the `&.` operator. There is always another way. You are probably breaking the [law of demeter](https://en.wikipedia.org/wiki/Law_of_Demeter)
- On the same note, if there is more than one dot in a line check very carefully that none of the return values are nullable
- default return values are the goods `return nullable || default_value`
