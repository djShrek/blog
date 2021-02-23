---
layout:     post
title:      "SOLID Principles in Ruby: Open Closed Principle Pt. 1"
date:       2020-09-15 20:27:00
author:     "bearcat"
---

The "O" in SOLID Principles represents the Open/Closed principle. This means that your code
should be "open for extension but closed for modification." But what does this 
look like in practice? Do we write classes that are never modified after they are written?
This blog post is the first of 3 examples of how we can apply the Open-Closed principle to our code.

The first example uses the Strategy Pattern. The Strategy pattern is a design pattern that lets
you modify the behavior of an object using another object at runtime. It is defined by using a set objects, or "strategies", that will generally adhere to the same interface and perform a similar job. 

The example I use will be an example of combining objects to create a type of Potion.
I will start off by creating a Potion class:

```Ruby
  class Potion
    attr_reader :ingredients

    def initialize(ingredients = [])
      @ingredients = ingredients 
    end

    def mix
      ingredients.each do |ingredient|
        ingredient.use
      end
    end
  end
```

As you can see, the Potion class takes an array of ingredients. It has only one other method, which is the "mix" method that iterates over each ingredient and also calls the "use" method. This sets up the interface that we expect each ingredient to share. Now we can combine any number of "ingredients" we see fit to create any number of types of potions. I will create 3 different ingredients as examples:

```Ruby
  module Ingredient
    class Health
      attr_reader :health_points 

      def initialize(health_points)
        @health_points = health_points 
      end

      def use
        puts "Increase health by #{health_points}"
      end
    end
  end

  module Ingredient
    class Mana
      attr_reader :mana_points

      def initialize(mana_points)
        @mana_points = mana_points 
      end

      def use
        puts "Increase mana by #{mana_points}"
      end
    end
  end

  module Ingredient
    class DragonBlood
      attr_reader :points_increase

      def initialize(points_increase)
        @points_increase
      end

      def use
        puts "Turn into dragon: Increase health and mana by #{points_increase} points"
      end
    end
  end
```
Then, to create a potion, I simply pass an array of whatever combination of ingredients I want.
Here are some examples:

```Ruby
  ingredients = []
  ingredients << Ingredient::Health.new(100)
  health_potion = Potion.new(ingredients)
  health_potion.mix
  # Increase health by 100

  ingredients = []
  ingredients << Ingredient::Mana.new(100)
  mana_potion = Potion.new(ingredients)
  mana_potion.mix 
  # Increase mana by 100

  ingredients = []
  ingredients << Ingredient::Health.new(500)
  ingredients << Ingredient::Mana.new(500)
  elixir = Potion.new(ingredients)
  elixir.mix
  # Increase health by 500
  # Increase mana by 500

  ingredients = []
  ingredients << Ingredient::Health.new(1000)
  ingredients << Ingredient::Mana.new(1000)
  ingredients << Ingredient::DragonBlood.new(2000)
  super_dragons_blood_potion = Potion.new(ingredients)
  super_dragons_blood_potion.mix

  # Increase health by 1000
  # Increase mana by 1000
  # Turn into dragon: Increase health and mana by 2000 points
```
By using the strategy pattern and passing in objects to change behavior, the context object (the Potion), doesn't need to know anything about its dependencies. This decouples the Potion class from
the Ingredient classes and allows me to combine these ingredients for an infinite number of potion types.
The Ingredient class is also decoupled from the Potion class and be used in other classes. For example, if you played the classic RPG Final Fantasy, you know there are potions that can increase your health and mana points. But there are also weapons, such as staffs, that can increase the health points of your characters. Imagine you that you wanted to create a Weapon class that can also take in ingredients that can apply a status effect such as a health point increase. Well now you can just reuse the Ingredient::Health class and just pass in the object to a Weapons class, making the Ingredient class reusable.

## Summary

As you can see in our example, the Potion class is never "opened" for modification, but instead its behaviors are extended with passing in the necessary objects. The behavior of the Potion is delegated to its ingredients where the ingredients do the actual work. It doesn't need to know anything about health, mana, dragon's blood etc. and the ingredients only need to implement a common interface. This makes separates the concerns of both objects and makes these classes flexible and robust. Another small but important benefit to this pattern is that each class focuses on a single responsibility, or the "S" in SOLID, so the Strategy Pattern actually represents two out of the 5 SOLID principles, but I wanted to highlight the pattern in the context of the Open-Closed principle. Other ways of changing an algorithm by using classes include the Template pattern, which uses inheritance instead of composition, but that would be for another post. 

Becoming 1% better every day!

