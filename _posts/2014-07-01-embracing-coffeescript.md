---
title: Embracing CoffeeScript
thumb: embracing-coffeescript-thumb.png
author: Chris
type: posts
---

Until quite recently, I was rather against the use of CoffeeScript. My typical responses would be, "Why would I need to use it when I already know how to do what it does for me" and "Have you seen the syntax!".

However, as a result of being pushed into trying it out, it turns out I actually love the simplicity of it. It takes care of a lot of the things that bother me about JS, with things like scoping, interhitance and closuring all being handled correctly.

These are all things I learnt to deal with in different ways using JS, but it always involved some pretty repetitive code and a lot of noise which made it hard to read 6 months later when you go back and wonder what the heck your code is doing.

Here are a couple of examples of the things I really like about it:

{% highlight coffeescript %}
# Classes
class Foo
  constructor: ->
    # this == @
    @test = true
    @foo = "foo"

    # "Fat" arrow (=>) deals with scoping of this
    $('#some-id').on "click", (ev) =>
      @test = false
      @foo = "Clicked"

      # Calling methods without brackets
      @someMethod @test, @foo

# Nice short hand for prototype + handling multiple arguments
Foo::someMethod = (args...) ->
  console.log(args)
{% endhighlight %}

vs the same thing in JavaScript:

{% highlight javascript %}
var Foo = (function() {
  function Foo() {
    this.test = true;
    this.foo = "Foo";

    var scope = this;
    $('#some-id').on('click', function(ev) {
      scope.test = false;
      scope.foo = "Clicked";

      scope.someMethod(scope.test, scope.foo);
    });
  }
  return Foo;
})();

Foo.prototype.someMethod = function() {
  var args;
  args = 1 <= arguments.length ? [].slice.call(arguments, 0) : [];
  return console.log(args);
};
{% endhighlight %}

Not to mention you can do class inheritance with the ability to call super etc.

At work we have started to use CoffeeScript now as a result of some of the initial testing that we did, and I've made some big pushes to convert alot of our existing JS codebase to CS - something which has trimmed a few thousand lines of code from our repository as a result of the cleaner code style.

#### Conclusion

Whilst CoffeeScript does not solve everything that is wrong with JavaScript, it certainly makes a big enough leap to make it useful and worth looking into. Once you get used to the syntax, it starts to feel so much easier.

I would definitely recommend trying out CoffeeScript, as it's easy to dismiss like I did at first. There are some good examples on the [CoffeeScript website](http://coffeescript.org/) which are worth taking a look at.
