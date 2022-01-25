## Goals
- Learn to use a TDD approach
- Learn how to use mocking in tests
- Have fun and solidify understanding of the above concepts
- Enjoy yourself!
  - Don't feel too much pressure with this.
  - You are free to reach out for assistance at any time, but I recommend giving things a shot before doing so just to help you learn to think through the ideas.

## Setup
  - [Sign up for the Cat Api](https://thecatapi.com/)
    - Note: You will receive an email with api key - save this
- Make sure you have rails 7 installed as well as ruby >= 3.1

## Create a new Rails project:
``rails new Catutorial -d postgresql``

## Switch to the newly created project folder:
``cd Catutorial``

## Make a commit:

- ``git add -A``
- ``git commit -m "initial commit"``

## Initialize the database:
``rails db:create``

## Start rails to test that the app is working so far:
``rails s``

## Stop once you verify the app is running.
# Next, Add the following to your gemfile:

```
group :development, :test do
  gem "debug", platforms: %i[ mri mingw x64_mingw ]
  gem 'approvals', '~> 0.0.25'
  gem 'rspec'
  gem 'rspec-rails'
  gem 'rspec-mocks'
  gem 'solargraph'
  gem 'pry-rails'
  gem 'pry-byebug'
end
```

## Execute the following commands:
- ``bundle install``
- ``rails g rspec:install``

## Make sure app is still working:
``rail s``

## If it is working, go ahead and stop the app and then commit again:

``git commit -m “Adding spec and debugging gems”``

## Create the following file in your spec folder:
cat_repository_spec.rb

## Add a describe block inside cat_repository_spec.rb
```
describe 'CatRepository' do
  describe 'get_cats' do
    it 'should return cats'
      expect(nil).to eq true
    end
  end  
end
```

# Run the tests
``bundle exec rspec``
- Tests should fail


## Create the following file inside the lib folder:
``cat_repository.rb``

## Create the class CatRepository inside this file:
```
class CatRepository
  def initialize()
  end

  def get_cats()
    nil
  end
end
```

## Update test
```
  it 'should return cats'
      #arrange
      cat_repository = CatRepository.new

      actual_result = at_repository.get_cats()
      expect(actual_result.length()).to > 0
    end
```

## Run tests again
``bundle exec rspec``
- The tests will fail again

# TO BE CONTINUED
