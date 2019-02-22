---
layout:     post
title:      "Learning how to use RSpec hooks, DatabaseCleaner gem, and let vs let! by doing."
date:       2018-09-18 9:30:00
author:     "bearcat"
---

The company that I do contract work for has a web application written in Ruby on Rails. To my surprise,
there were almost no unit tests around any of the models or controllers. Even worse was
that the code was not written to be developer friendly as the code was littered with
long 1 liners and obscure variables like 'obj' and 'a.' I was eager to begin backfilling
the codebase with some unit tests so I could do some refactoring, but quickly came across an annoying spec failure
that forced me to really study how RSpec and the DatabaseCleaner gem work in conjunction.

What I am actually trying to test currently doesn't matter. The issue I was encountering was my
lack of understanding of how to properly setup my spec. In my RSpec file, there were two tests
that used the same helper method that would represent a Store. I used the FactoryGirl gem to create
a "Store" factory. The "Store" AR model had validation on its "name" column and I used the Faker gem
to generate a random name for me on the Store instance. The "store" would be created by let! helper
method prior to any of the specs running as stated in the RSpec documention:

> Use let to define a memoized helper method. The value will be cached
across multiple calls in the same example but not across examples.
Note that let is lazy-evaluated: it is not evaluated until the first time
the method it defines is invoked. You can use let! to force the method's
invocation before each example.

And my spec file looked something this:

```ruby

let!(:store) { create(:store) }

it "first test" do
  # example omitted
end

it "second test" do
  # example omitted
end
```

The first spec would pass but the second would immediate fail with this message:

```
Failure/Error: let(:store) { create(:store) }
     ActiveRecord::RecordInvalid:
       Validation failed: Name has already been taken
```

So this suggested to me that the Store being created in the first spec was being persisted
through the next spec. According to the RSpec documentation above, the let! forces the method
invocation before the example, which is fine, but shouldn't it create a _new_ instance of Store in each example
and shouldn't the Store instance in the previous example should have been deleted?

To figure that out, I had to check my DatabaseCleaner gem settings. The DatabaseCleaner gem provides a set of
strategies for cleaning your database, but more specifically, to ensure a clean state between running tests.

So I look at my RSpec config file for the gem setting's and find:

```ruby
  config.before(:suite) do
    DatabaseCleaner.clean_with(:truncation)
  end

  config.before(:each) do
    DatabaseCleaner.strategy = :transaction
  end

  config.before(:each) do
    DatabaseCleaner.start
  end

  config.around(:each) do |example|
    DatabaseCleaner.cleaning do
      example.run
    end
  end

  config.after(:each) do
    DatabaseCleaner.clean
  end
```

So now, I have to figure out several things. First, what do the different DatabaseCleaner
methods like #clean_with, #start, #cleaning, and #clean do? And second, when do these
RSpec hooks of before, around, after all run relative to each other and what is the difference
between the :suite and :each options? And finally, what is the difference between
the two database cleaning strategies of truncation and transaction?
