# Procedural Vs Object-Oriented Ruby

## Overview

When I first learned about Object Orientation I was a pretty inexperienced and novice programmer. But I had built some complex financial models using procedural code and Object Orientation confused me. I found myself wondering "Why do I need all this architecture and structure - I can manage my own code."

As my applications became more complex though, especially as I integrated more interfaces like rich web interfaces, I struggled to produce reliable and easy to modify code. And then Object Orientation clicked for me.

An object can be defined as a piece of code that contains all the data and all the logic to accomplish a job. Whereas procedural programming uses procedures to operate on data structures, object-oriented programming bundles the two together so an "object" operates on its "own" data structure.

Consider the displaying a tic tac toe board, checking the current player, and knowing the turn count of a game in Tic Tac Toe.

Procedural:
```ruby
board = Array.new(9, " ")

def current_player(board)
  turn_count(board) % 2 == 0 ? "X" : "O"
end

def turn_count(board)
  board.count{|token| token == "X" || token == "O"}
end

def display_board(board)
  puts " #{board[0]} | #{board[1]} | #{board[2]} "
  puts "-----------"
  puts " #{board[3]} | #{board[4]} | #{board[5]} "
  puts "-----------"
  puts " #{board[6]} | #{board[7]} | #{board[8]} "
end
```

The thing you notice is that the state of the game, represented by the `board` array, is defined outside of any code that directly relates to Tic Tac Toe. We are basically using the proximity of the variable declaration to the methods as a way to say that these methods and data are related. That is a weak convention.

You'll also notice that we constantly have to pass around `board` to every method. That is tedious and potentially very troublesome as any method can modify that variable and continue passing it around causing errors.

Ultimately, we don't want to manage our data manually through arguments and proximity, we want to teach our object to do that. Consider a Object Oriented implementation of the example from above.

```ruby
class TicTacToe
  def initialize(board = nil)
    @board = board || Array.new(9, " ")
  end

  def current_player
    turn_count % 2 == 0 ? "X" : "O"
  end

  def turn_count
    @board.count{|token| token == "X" || token == "O"}
  end

  def display_board
    puts " #{@board[0]} | #{@board[1]} | #{@board[2]} "
    puts "-----------"
    puts " #{@board[3]} | #{@board[4]} | #{@board[5]} "
    puts "-----------"
    puts " #{@board[6]} | #{@board[7]} | #{@board[8]} "
  end
end
```  

Notice that every method became easier to understand. They no longer require arguments and instead can rely on the internal state of the object. That makes the code easier to maintain and to extend.

## Moving from Procedural to Object Oriented

The things you want to look for when refactoring procedural code into object-oriented code are:

1. Find any data the methods rely on. Does this data belong outside the object, to be passed in on initialization, or can the object instantiate this data itself?

2. Which of your methods are using arguments to pass data around scopes and could they instead just read the data from the internal state of the object?

3. What un-encapsulated procedural code is part of your program (random lines of code not contained in a method) and does that code belong as a behavior of your object?

Anything that works procedurally can also work in an Object Oriented fashion and being able to move between these two styles of programming is crucial.
