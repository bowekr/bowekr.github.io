Ruby on rails Callback

**Bad Code**


```ruby
def update
	@zombie = Zombie.find(params[:id])
	if @zombie.age > 20
		@zombie.rotting = true
	end
end
```
#
# lets kita pindahkan logic ini ke model
#

##
# Good Code
# - Model
##
class Zombie < ActiveRecord::Base
	before_save :make_rotting

	def make_rotting
		self.rotting = true if age > 20
	end
end
##
# All Callback
before_validation
after_validation

before_save
after_save

before_create
after_create

before_update
after_update

before_destroy
after_destroy


#
# More Example
#
# Objective :
# Create a before_save callback that checks to see if a tweet has a location, 
# if it does have a location then set show_location to true.
# Tip: You can check to see if location exists with if self.location?
# Answer :
class Tweet < ActiveRecord::Base
  before_save :check_location

  def check_location
    if self.location?
      self.show_location = true
    end
  end
end
