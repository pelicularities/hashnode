## How does the spaceship operator <=> work?

*Note: the spaceship operator `<=>` exists in a number of programming languages including C++, Perl, PHP and Groovy, but this article will discuss it in the context of Ruby, just because that's what I'm more familiar with.*

The spaceship operator `<=>` performs what’s known as a [three-way comparison](https://en.wikipedia.org/wiki/Three-way_comparison). Its basic usage is simple:

```
a <=> b
1 <=> 2 # returns -1 if a < b
3 <=> 3 # returns 0 if a == b
5 <=> 4 # returns 1 if a > b
```

That’s it.

## Why use it?
You’ve probably written some version of this code before:

```
if a < b
  puts "#{a} is smaller than #{b}!"
elsif a > b
  puts "#{a} is larger than #{b}!"
else
  puts "#{a} is equal to #{b}!"
end
```

You can do the same thing with the spaceship operator:
```
case a <=> b
when -1
  puts "#{a} is smaller than #{b}!"
when 1
  puts "#{a} is larger than #{b}!"
when 0
  puts "#{a} is equal to #{b}!"
end
```

Okay, but that’s not obviously better than using an `if-elsif-else` block. In fact, it’s one line longer. However, there are nearly identical situations when using `<=>` and `case`/`when` looks a bit more readable. 

Compare these two blocks of code:

```
# a and b are both strings
if a.length < b.length
  puts "#{a} is shorter than #{b}!"
elsif a.length > b.length
  puts "#{a} is longer than #{b}!"
else
  puts "#{a} is as long as #{b}!"
end
```

```
# a and b are both strings
case a.length <=> b.length
when -1
  puts "#{a} is shorter than #{b}!"
when 1
  puts "#{a} is longer than #{b}!"
when 0
  puts "#{a} is as long as #{b}!"
end
```

A minuscule gain in readability and maintainability. Big whoop.

## Sorting and comparison
Let’s get to the real reason the spaceship operator matters in Ruby: it’s used whenever Ruby wants to compare two things.

Ruby’s [`sort`](https://ruby-doc.org/core-3.0.0/Enumerable.html#method-i-sort) method takes a block that must implement a comparison between two elements, `a` and `b`. The block must return:
- `-1` when `a` comes before `b`
- `1` when `a` comes after `b`
- `0` when the two values are equal

You don’t *need* to use the spaceship operator to accomplish this, but it’s the simplest way to do so.

To begin with, let’s look at sorting an array of numbers from smallest to largest using a block:

```
array = [2, 3, 1]
sorted = array.sort { |a, b| a <=> b }
```

(Ruby’s `sort` method uses the [quicksort](https://en.wikipedia.org/wiki/Quicksort) algorithm, but the following example is a [bubble sort](https://en.wikipedia.org/wiki/Bubble_sort). That’s fine, the key idea we’re trying to understand here is the `<=>` operator, which works the same no matter which sorting algorithm we use.)

We’ll do our first pass through the array and compare the first two elements:
- assign the first element `2` to the variable `a`
- assign the second element `3` to the variable `b`
- evaluate `a <=> b`: ` 2 <=> 3`
- this returns `-1`, since `2` comes before `3`, so we don’t have to  rearrange `2` and `3`

Let’s look at the next pair:
- assign the second element `3` to `a`
- assign the third element `1` to `b`
- evaluate `a <=> b`: `3 <=> 1`
- this returns `1`, which means that `3` should come after `1`, and we need to reverse `3` and `1`. 

That gives us an array of `[2, 1, 3]` after the first pass.

Now, we go for our second pass through the array:
- assign the first element `2` to the value `a`
- assign the second element `1` to the value `b`
- evaluate `a <=> b`: `2 <=> 1` 
- this returns `1`, meaning that `2` should come after `1`. We switch `2` and `1`, and now our array is `[1, 2, 3]`

Let’s do a third pass through the array to check if we need to make any more switches:

|`a`|`b`|`a <=> b`|result|
|:---:|:---:|:---:|:---:|
|`1`|`2`|`1 <=> 2`|`-1`|
|`2`|`3`|`2 <=> 3`|`-1`|

When the array is sorted, the given expression in the block (in this case `a <=> b`) will always evaluate to `-1`.

### Once more, backwards
What if you wanted to sort the array from largest to smallest? It’s a simple change:

```
array = [2, 3, 1]
sorted = array.sort { |a, b| b <=> a }
```

Now, when we make our first pass through the array:
- assign the first element `2` to the variable `a`
- assign the second element `3` to the variable `b`

Instead of `a <=> b`, this time we sort based on the result of `b <=> a`:
- evaluate `b <=> a`: `3 <=> 2` 
- this gives us a result of `1`, which tells us that `2` should follow `3`.

And now, if we go through the array and evaluate `b <=> a` for each pair, we see that it always evaluates to `-1`.

|`a`|`b`|`b <=> a`|result|
|:---:|:---:|:---:|:---:|
|`3`|`2`|`2 <=> 3`|`-1`|
|`2`|`1`|`1 <=> 2`|`-1`|

## The Comparable mixin
Suppose you’re writing a class for a Player model that looks like this:

```
class Player
  attr_accessor :name, :score
  def initialize(attributes)
    @name = attributes[:name]
    @score = attributes[:score]
  end
end
	
player1 = Player.new(name: 'Alice', score: 1000)
player2 = Player.new(name: 'Bob', score: 3000)
player3 = Player.new(name: 'Charlie', score: 2000)
players = [player1, player2, player3]
```

You want to be able to quickly sort players by score, with the best scores first. Of course, you can do this:

```
players_sorted = players.sort { |a, b| b.score <=> a.score }
```

This would get old real quick. Instead, let’s write our own `<=>` method for the `Player` class: 

```
class Player
  attr_accessor :name, :score
  def initialize(attributes)
    @name = attributes[:name]
    @score = attributes[:score]
  end

  def <=>(other_player)
    score <=> other_player.score
  end
end
```

This tells Ruby that when two `Player` instances are compared using the `<=>` operator, Ruby should compare the players’ `score` results. Now we can simply do this to sort players from highest scores to lowest:

```
players_sorted = players.sort { |a, b| b <=> a }
```

This makes life a little easier for us. However, we can go further than this. Ruby has a mixin called [Comparable](https://ruby-doc.org/core-2.5.0/Comparable.html), which can be included in any class that defines a `<=>` method:

```
class Player
  include Comparable
  attr_accessor :name, :score
  def initialize(attributes)
    @name = attributes[:name]
    @score = attributes[:score]
  end

  def <=>(other_player)
    score <=> other_player.score
  end
end
```

This gives us access to [a bunch of useful methods](https://ruby-doc.org/core-2.5.0/Comparable.html) that depend on the spaceship operator, including `<`, `<=`, `>`, and `>=`. This means that we can now do something like this:

```
if player1 > player2
  puts "#{player1.name} leads #{player2.name}!"
end
```

Note that Comparable will also give the class a `==` method based on the result of `<=>`. Be prepared for this behaviour:

```
player3 = Player.new(name: 'Charlie', score: 2000)
player4 = Player.new(name: 'Eve', score: 2000)

puts player3 == player4 #=> prints 'true'
```

## Round-up
I wanted to write this post because I felt that I understood the  spaceship operator, but I couldn’t explain it very well. Hopefully this gets you started with using the `<=>` operator, and including the Comparable mixin into classes where it might be useful.

If you have any suggestions or edits, please let me know!