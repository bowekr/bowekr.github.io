---
layout: default
title: My Ruby Guidelines
---
Oke, kali ini gue mau Challenge diri gue sendiri untuk merubah prinsip coding gue dengan membuat Guidelines,
So Guidelines yang gw buat disini semuanya adalah dari hasil gw resaerch, dan gw ambil inti tiap research gue,
dan jadilah Guidelines ini .


1. Sebuah Class tidak boleh lebih dari 100 Line.
2. Sebuah Method tidak boleh lebih dari 10 Line.
3. Sebuah Method name, variable or process tidak boleh lebih dari 80 Character.
4. Penamaan sebuah Method harus mewakilkan fungsi nya.
5. Sebuah conditional statement yang pembandingan nya lebih dari 2, maka harus di buat method



```ruby
class ProjectsController
  def index
    # When user is admitted at least a week ago we show its active projects
    if current_user && current_user.created_at < (Time.now - 7*24*3600)
      @projects = current_user.active_projects

    # If not admitted we show some featured projects, and set a marketing flash
    # message when user is new
    else
      if current_user
        @flash_msg = 'Sign up for having your own projects, and see promo ones!'
      end
      @projects = Project.featured
    end
  end
```

We need to refactor 

```ruby

require_relative 'setup'

# Intention Revealing Method
# Extract relevant concepts into methods or variables with proper names
# Code should explain itself

class ProjectsController
  def index
    if user_is_admitted_at_least_a_week_ago?
      @projects = current_user.active_projects

    else
      if user_is_new?
        show_marketing_flash_message
      end

      @projects = Project.featured
    end
  end

  private

  def user_is_new?
    current_user && current_user.created_at > a_week_ago
  end

  def user_is_admitted_at_least_a_week_ago?
    current_user && current_user.created_at < a_week_ago
  end

  def show_marketing_flash_message
    @flash_msg = 'Sign up for having your own projects, and see promo ones!'
  end

  def a_week_ago
    Time.now - 7*24*3600
  end
end
```


Ke 4 Guidelines ini sudah mencakup banyak aspek.


1. Maintainability
2. Readability
3. Modular
4. Scalability
5. Performance


Feel free to ask.