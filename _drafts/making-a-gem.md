---
layout:     post
title:      "Learning to create my first Gem"
date:       2019-08-24 2:35:00
author:     "bobby"
---

Part of my study work flow is using a flash card software called Anki. Anki helps create virtual flash cards as study material so you can review what you have learned. Creating the flash cards one by one is what one usually would do, but I like to also
review the card question and answers before I create them. So what I would do is type out each question and answer
for any card that I wanted to create in a Quip file and then later go back and copy-and-paste each Q/A into the Anki software.
This process got too tedious, so I decided to look up if there was an easier way to create cards such as importing
a file into the software and bulk creating all the cards at once. Luckily, the Anki software does 
allow you to import a text file to create flash cards. However, I wanted to take this one step further
and use a YAML file format because the YAML format is easier for me to read and allows me to store data
in a file that I can use later for other purposes other than creating a flash card (maybe simply importing to
Quip for notes or something). 

This led to create a Ruby CLI gem that did two things: generate a boilerplate
YAML file and be able parse that file into an Anki text file ready for import. 
(Why create a Ruby gem you ask? The answer can be found [here.](https://bundler.io/v1.12/guides/creating_gem.html#but-first-why))

A Ruby gem is generally a Ruby program or packaged library. It usually contains files of code that
drive the library logic, tests, config files, etc. To create my gem I used a combination of the Bundler and Thor gems.

First, the gem is creating using the bundler command:

```
  bundle gem ank3
```

which will create a bunch of boilerplate files for you. I called my name gem "ank3" because as of this writing, there are two gems already called
"Anki" in Rubygems. I figured I tried to be clever and call it "Ank3" in honor as being the third gem based off Anki. 

Next, I decided to go the TDD route and begin with writing a few tests for the core interface of the gem. So I create a directory for my specs and add RSpec as a dependency to my ank3.gemspec file. Then I create a ``` ank3_spec.rb ``` file and start writing my tests. At this point, I know I want my CLI to do things:

1. Convert my YAML file to a file format that can be imported to Anki
2. Generate a boilerplate YAML file that is ready to accept questions and answers (and tags in the future).

From the Anki [documentation](https://apps.ankiweb.net/docs/manual.html#importing), any plain text file that contains
fields separated by commas, semicolons or tabs can be imported into Anki. So an example file that can be used to import into Ank3 would look like this:

```
What is 1+1; Two 
What is an example of a fruit?; Apple
```

This would create two cards, with question and answer respectively. 

So I start by writing test for a basic class that will represent the Card: 

```ruby
  describe "Ank3::Card" do
    context "convert" do
      it "converts data to a string" do
        expect(Ank3::Card.new(data).convert).to eq "What is 1+1?; Two\n"
      end
    end
  end
```

Then I create the class and augment my spec file to make the test pass:

```ruby
  module Ank3
    class Card
      attr_reader :data

      def initialize(data)
        @data = data
      end

      def convert
        "#{front}; #{back}\n" 
      end

      def front
        data["front"]
      end

      def back
        data["back"]
      end

      def tags
        data["tags"]
      end
    end
  end
```

and

```ruby
  let(:data) do
    {
      "front" => "What is 1+1?",
      "back" => "Two"
    }
  end

  describe "Ank3::Card" do
    context "convert" do
      it "converts data to a string" do
        expect(Ank3::Card.new(data).convert).to eq "What is 1+1?; Two\n"
      end
    end
  end
```

I expect the card class to have one public method, and that method simply converts a hash of question and answer to a string. Also notice that I add a new line character (\n) at the end of the string. This demarcates the end of a card
and will be important when we combine all the converted strings in a single file.

<!-- What is preventing me from writing?
- It's not interesting - How do you know it's not interesting? Make it interesting. How can I make it interesting?
- It's not useful - How do you know it's not useful? If you use it, it's useful.
- It's too much effort - What is better than writing and reviewing and talking about what you have worked on?
- It's going to take too long - Writing and mastering a topic takes time
- It's not worth the effort - Then what is?
- The gem is not useful
- I have to repeat and recreate all my steps, which takes away time from something else
- I'm never going to finish it
- I don't know what to write about
- I don't know what's important in a blog post  
->

<!-- Why YAML?

Things I learned:

1. Setting up the gem with Bundler
2. Writing the code
3. Learning to use Thor
4. Learning how to use other libraries:
    - JSON
    - YAML
    - Writing to a file
    - Difference between require and require_relative
    - Semantic versioning
    - How to install Linux on windows so I can run the gem
    - The future: 
      - Build API to create cards

-->

