1. How to create validation with reg_exp which can accept nil?
        
        validates :field,
          format: { with: /\A([a-z]+|)\z/i }, :allow_blank => true
2. How you can create references to some model?
        
         # where main_photo_id == current_class_object.id
         has_one :main_photo, class_name: 'Photo', foreign_key: "main_photo_id", dependent: :destroy
3. How to generate model inside namespace in rails?
        
        rails generate model namespace_name/model_name
        # NameSpace::Model.create(title: 'hge2')
4. How to validate number beetween 2 values?

         validates :amount, numericality: {greater_than_or_equal_to: 0, less_than_or_equal_to: 100}
5. How to set new db table to model?
        
        class MyBook < ApplicationRecord
          self.table_name = 'books'
        end
6. How to get access to hellpers from the model?
        
        class Book < ApplicationRecord
          def self.helper
            ActionController::Base.helpers
          end
        end
        
        Book.helper.link_to "any_link", "/"
7. How to return object attributes like a hash?
        
        Book.last.attributes
        => it return hash attributes
8. How to generate a model without migration?

```ruby
   rails g model Animal --skip-migration
   #or
   rails g model Animal --migration=false
   
```

9. How to generate a model with a parent?

```ruby
   rails g model Animal --parrent=BaseAnimal
```
