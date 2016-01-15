---
layout: post
title: coding challenge => find the product of every integer except the integer at that index
comments: true
permalink:
---

#####That title is a mouthful; say it 5x fast...go. Jk. Below is how I went about solving this Q, written lovingly in Ruby.

<br>
Here's the skinny: we are gonna' need to write a function/method that takes in an array of integers for the argument and returns an array of the products (those integers multiplied with each other).
<br>

What really helps me is knowing what the expected output is going to look like when this method returns from doing its thing. What this question wants is something along these lines:


{% highlight ruby linenos %}
# Imagine this is what we start with
[2, 6, 3, 5]

# This is what the method should return
# Order doesn't matter here, as long as the array
# has these values
[36, 60, 30, 90]

# The method gets there by calculating this
[6*3*5, 2*3*5, 2*6*5, 2*6*3]
{% endhighlight %}

Feast them eyes on my solution. Don't worry if this looks cray cray or confusing, I'll explain it all the best I can. I also used long and descriptive variable names so others can quickly figure out what's going on with the code. **When I refer to line #'s, use the code snippet below.**

<br>
<br>
{% highlight ruby linenos %}
def get_product_of_all_ints_except_at_index(start_array)
  final_array_of_products = []
  num_of_combos_needed = (start_array.length - 1)
  all_combos = start_array.combination(num_of_combos_needed).to_a

  all_combos.each { |combo| final_array_of_products << combo.reduce(:*) }

  final_array_of_products
end
{% endhighlight %}
<br>
<br>

I knew that I was going to have to iterate through the <code>start_array</code>. But how? Was I going to use <code>Enumerable#each_with_index</code>? Sounds reasonable. Got me thinking though: I need combinations. That's the key to this problem.

Does the <code>Array</code> class have something already baked in to help with combinations? Does the <code>Enumerable</code> class?

Using Google-Fu, I came across this from the Ruby Documentation: [Array#Combination](http://ruby-doc.org/core-2.2.0/Array.html#method-i-combination). Like, omg. That's exactly the type of behavior I want. It even has helpful examples on how to use it: noice!

{% highlight ruby linenos %}
# From Ruby Docs
a = [1, 2, 3, 4]
a.combination(1).to_a  #=> [[1],[2],[3],[4]]
a.combination(2).to_a  #=> [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
a.combination(3).to_a  #=> [[1,2,3],[1,2,4],[1,3,4],[2,3,4]]
a.combination(4).to_a  #=> [[1,2,3,4]]
{% endhighlight %}

I know I needed a combination of three (since we're starting with 4 elements in the array), but what if the initial <code>start_array</code> has more integer elements inside it besides 4? Wouldn't it be neat-o if, in the future, we can supply this method with an array of *ANY* amount of integers *AND* have it return what we expect?!

{% highlight ruby linenos %}
# Boom! Now we'll get just the right amount of combinations
num_of_combos_needed = (start_array.length - 1)
{% endhighlight %}

Stepping through the <code>get_product_of_all_ints_except_at_index</code> method so far, I first declared the variable <code>final_array_of_products</code> which references an empty array (I'll use this later). Then <code>line 3</code> takes the <code>start_array</code>'s length and subtracts 1 so we will always get the perfect amount of combinations; that value is referenced via the <code>num_of_combos_needed</code> variable.

On <code>line 4</code>, the <code>start_array</code> calls the <code>combination</code> method, supplies it with the variable <code>num_of_combos_needed</code>, which works its lovely combo magic, and finally there's the <code>to_a</code> call at the end.

What <code>to_a</code> does is convert the calling object (in our case <code>start_array</code>) to an array. If we didn't have that conversion to an array, the return value of the <code>combination</code> method is an Enumerable object and that just won't cut the mustard. All of that is then referenced too via the <code>all_combos</code> variable.

{% highlight ruby linenos %}
# 'all_combos' will now reference [[2, 6, 3], [2, 6, 5], [2, 3, 5], [6, 3, 5]]
all_combos = start_array.combination(num_of_combos_needed).to_a
{% endhighlight %}

What we have now with the <code>all_combos</code> variable is 1 outer array with 4 little arrays inside it. On <code>line 6</code>, I iterate through those 4 little arrays and use Ruby's helpful <code>Enumerable</code> method <code>reduce</code> on each little array.

What does the <code>reduce</code> method do? Always, always check the [ruby documentation](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-reduce). It has everything you need, especially helpful examples.

{% highlight ruby linenos %}
all_combos.each { |combo| final_array_of_products << combo.reduce(:*) }
{% endhighlight %}

The above code is saying "Yo, for every little array inside of <code>all_combos</code>, multiply all the elements into one number via <code>reduce</code>, and then push that number into the <code>final_array_of_products</code> array via the <code><<</code> (shovel) operator."

Finally, on <code>line 8</code>, we have the <code>get_product_of_all_ints_except_at_index</code> method return <code>final_array_of_products</code> variable which references that once empty array with 4 numbers inside.

{% highlight ruby linenos %}
# This gets returned from the method when the dust settles
final_array_of_products  # => [36, 60, 30, 90]
{% endhighlight %}

Hope this helps. Stay turnt.
