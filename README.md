## Goals
- Learn about
  - TDD approach
  - Separation of concerns
  - Single repsonsibility principle
  - Using mocking in tests
  - Have fun!
- Remember... Enjoy yourself!
  - Don't feel too much pressure with this.
  - You are free to reach out for assistance at any time, but I recommend giving things a shot before doing so just to help you learn to think through the ideas.

## Setup
  - [Sign up for the Cat Api](https://thecatapi.com/)
    - Note: You will receive an email with api key - save this
- Make sure you have rails 7 installed as well as ruby >= 3.1

## Create a new Rails project:
``rails new Catutorial -d postgresql -T -G``
- -d sets the database you would like to use for the project. In this case postgresql.
- -T prevents the default test folder from being generated since we'll be using rspec
- -G skips setting up a git repository since you've probably already cloned this one.

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
# Next, Add the following to the existing section in your Gemfile:

```
group :development, :test do
  gem "debug", platforms: %i[ mri mingw x64_mingw ]
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
  describe 'get_categories' do
    it 'should return cats' do
      expect(nil).to eq true
    end
  end  
end
```

# Run the tests:
``bundle exec rspec``
- Tests should fail


## Create the following file inside the lib folder:
``cat_repository.rb``

## Create the class CatRepository inside this file:
```
class CatRepository
  def initialize()
  end

  def get_categories()
    nil
  end
end
```

## Update 'should return cat categories' test in cat_repository_spec.rb:
```
it 'should return cat categories' do
    #arrange
    cat_repository = CatRepository.new

    #act
    actual_result = cat_repository.get_categories()

    #assert
    expect(actual_result.length()).to > 0
end
```

## Run tests again:
``bundle exec rspec``
- The tests will fail again

## Add an API_URL and API_KEY constants to the top of CatRepository class:
```
API_URL = 'https://api.thecatapi.com/v1/'
API_KEY = 'your-api-key-goes-here'
```
- Note: This is not an ideal way to manage configuration, but it will do for now.

## Implement make_request, generate_url and default_headers in at the bottom of the CatRepository class in a private section:
```
def make_request(path:, headers:, params: {})
  JSON.parse(
    RestClient::Request.execute(headers: headers, method: :get, url: generate_url(path, params)),
    { :symbolize_names => true }
  )
end

def generate_url(path, params)
  "#{API_URL}#{path}#{'?' + params.to_param unless params.empty?}"
end

def default_headers()
  {
    'x-api-key': API_KEY,
    'content-type': 'application/json',
  }
end
```

## Implement get_categories in CatRepository class:
```
def get_categories()
    make_request(path: 'categories', headers: default_headers())
end
```

## Run Rspec to verify test still failing:
``bundle exec rspec``

## Update test to a hopefully passing state:
```
it 'should return cat categories' do
  # arrange
  cat_repository = CatRepository.new

  # act
  actual_result = cat_repository.get_categories()

  # assert
  expect(actual_result.length()).to be > 0
end
```

## Run Tests:
``bundle exec rspec``

## Checkpoint
- Congrats! You've got a working test using the actual API.
- We'll now move on to leveraging this call we've implemented.
  
# TO BE CONTINUED
