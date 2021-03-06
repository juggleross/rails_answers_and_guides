0. How to get show the source of a method?
            
            ActiveRecord::Base.method(:find).source_location
1. How can you check the data?
            
            user = User.new(name: "Michael Hartl", email: "mhartl@example.com")
            user.valid?
2. How you can allow access to 'user' attributes?
            
            user.name
            user.email
3. How you can find object by id?
            
            User.find(1)
4. How you can find object by attribute?
            
            User.find_by(name: 'vlad')
5. How you can select all user? last user? first user?
            
            User.all
            User.last
            User.first
6. Hou you can update attributes? 
            
            # 1 way
            user.email = "foo@bar.com"
            # 2 way 
            user.update_attribute(:name, "El Duderino")
            # for multiply
            user.update_attributes(name: "The Dude", email: "dude@abides.org")
7. How you can reload object? 

            user.reload
8. How you can see errors messages?
            
            user.errors.full_messages
9. How you can check if user has error?
            
            @user.errors.any?
10. How you can delete object?
            
            User.find(params[:id]).destroy
11. How you can delete table from database?
            
            $rails console
            # Then just type:
            ActiveRecord::Migration.drop_table(:users)
            
            # Where :users is the table name
12. How you can add column to existing table?
            
            #Use this command at rails console
            rails generate migration add_fieldname_to_tablename fieldname:string
            # and
            rake db:migrate 
13. How you can add index to existing column?
            
            rails generate migration AddIndexToTable
            # and change
            class AddIndexToTable < ActiveRecord::Migration
              def change
                add_index :table, :column_name
              end
            end
14. How to get access to the references params?
            
            # user belongs_to role, role has_many :users
            user.role.any_params

14. How to remove index from column?
            
            remove_index :table, :column

16. How to create many_to_many polimorphic accociation?
            
            # asigment.rb
            class Asigment < ApplicationRecord
              belongs_to :patient
              belongs_to :doctor_entity, :polymorphic => true
            end
            
            # doctor.rb
            class Doctor < ApplicationRecord
              has_many :asigments, as: :doctor_entity
              has_many :patients, through: :asigments
            end
            
            # stomotolog.rb
            class Stomotolog < ApplicationRecord
              has_many :asigments, as: :doctor_entity
              has_many :patients, through: :asigments
            end
            
            # patient.rb
            class Patient < ApplicationRecord
              has_many :asigments
              has_many :doctors, through: :asigments, :source => :doctor_entity,
                :source_type => 'Doctor'
              has_many :stomotologs, through: :asigments, :source => :doctor_entity,
                :source_type => 'Stomotolog'
            end
            
            # migration all ordinary, without this
            class CreateAsigments < ActiveRecord::Migration[5.0]
              def change
                create_table :asigments do |t|
                  t.belongs_to :patient, index: true
                  t.references :doctor_entity, polymorphic: true, index: true

                  t.timestamps
                end
              end
            end


16. How to drop test environment data_base?
           
           bundle exec rake db:drop RAILS_ENV=test
           bundle exec rake db:create RAILS_ENV=test
17. How you can create collback with check old value?
            
            # So if you have an attribute total, you will have a total_changed? method and a total_was method that returns the                  old value.
            after_update :send_message_to_user
              private

                          def send_message_to_user
                              if self.status_changed?
                                if self.status_was == 'declined' && self.status == 'accepted' 
                                  puts 'changed'
                                end
                            end
                          end
18. How to add addition condition to has_many field?
           
           # adding where
           has_many :unauthorized_friends,  -> { where(friendships: { authorized: true}) }, :through => :friendships, :source => :user
19. How to create Self-Referential Association?
            
            #user.rb
            has_many :friendships
            has_many :friends, :through => :friendships
            
            has_many :unauthorized_friends,  -> { where(friendships: { authorized: true}) }, :through => :friendships, :source => :user
            # friednship.rb
            belongs_to :user
            belongs_to :friend, :class_name => "User"
            
            # inside db
            class CreateFriendships < ActiveRecord::Migration[5.0]
              def change
                create_table :friendships do |t|
                  t.integer :user_id
                  t.integer :friend_id
                  # add addition field for adding new condition and type if friends
                  t.boolean :authorized, :default => false
                  
                  t.timestamps
                end
              end
            end
20. Flaot value in activerecord?
            
            decimal
21. How to set uniqunes for several model?
            
              validates :name, uniqueness: { scope: :estate_id }
22. How to set after_update callback with condition?
            
            before_save :do_something, if: :status_id_changed?
24. How to select uniq value from active record models?
                        
            user.addresses.pluck(:city).uniq # => ['Moscow']
25. How you can group by multiply variables?
            
            @bunch.group_by{|e| [e.commentable_id, e.commentable_type]}
26. How you can set another name for one table and set references?
            
              # add to model
              belongs_to :author, class_name: "User"
              
              # generate miration
              def change
                add_reference :tickets, :author, index: true
                add_foreign_key :tickets, :users, column: :author_id
              end
27. How you can create has_and_belongs_to_many association?
            
            1. # add to class
              class Actor < ApplicationRecord
                has_and_belongs_to_many :movies
              end
            
              class Movie < ApplicationRecord
                has_and_belongs_to_many :actors
              end
            
            2.# Then generate migration 
              rails g migration CreateJoinTableActorMovie actor movie
               
              # Migration has such view
              def change
                create_join_table :actors, :movies do |t|
                  t.index [:actor_id, :movie_id]
                  t.index [:movie_id, :actor_id]
                end
              end
           
           3. # Now you can add new values
           
            movie = Movie.find(params[:id])
            actor = Actor.find(params[:promo_id])
            movie.actors << actor
            

28. How you can compare Date?

            .where('created_at <= ?', Time.now)
29. How you can create transaction? (only perform when all action succeed as one action)
            
            ActiveRecord::Base.transaction do
              david.withdrawal(100)
              mary.deposit(100)
            end
30. How you can increment some values in model?

            a = Article.first
            a.increment!(:view_count)
            a.reload.view_count # -> 1
31. How you can check if object exists?
            
            # where coupon is ActiveRecord model
            Coupon.exists?(status: :unactivated)
            
32. How you can find values inside associative tables?
            
            # just include this table
            Monument.joins(:categories).where(categories: {name: ["World War II", "Колонны"]})
33. How you can all values only by part words?
            
            where("first_name LIKE  ?", "%#{first_name}%")
34. How you can correctly write method where with optional params?
            
            http://brendankemp.com/essays/build-a-query-in-activerecord-from-optional-params-the-non-hideous-version/
35. Select where clause with multy variable, return exactly variable?
            
            Person.joins(:books).where("books.id IN (?)", [1,2,4]).group(:id).having('count(books.id) = ?', a)
36. Rails order by results count of has_many association

            Company
              .left_joins(:jobs)
              .group(:id)
              .order('COUNT(jobs.id) DESC')
37. How you can make case-unsensitive search in Rails?
            
            Product.where('lower(name) = ?', name.downcase)
38. How you can search on multiply attributes?
            
            Model.where("lower(first_name || ' ' || last_name) LIKE ?", "%#{search.downcase}%")

39. How to get time before some second from created_at?
            
            MyModel.where("created_at < ?", 2.days.ago)
40. Hwo to update attributes without rewriting db?
            
            my_obj.write_attribute(:my_field, 'some value')
## ------------------------ ActiveRecord without rails ------------------------


1. How you can use ActiveRecord with some db without rails?
            
            # create file test_without_rails.rb
            
            require 'active_record'

            ActiveRecord::Base.establish_connection({
              adapter: 'postgresql',
              encoding: 'unicode',
              username: 'postgres',
              host: 'localhost',
              database: 'myapp_development'
            })

            class Thing < ActiveRecord::Base
              # set table which already exists here
              self.table_name = "users"
            end

            Thing.create(name: "vlad")
2. Article about using ActiveRecord without rails?

            http://ashleyangell.com/2015/05/estabilishing-activerecord-database-connections-in-ruby-but-without-rails/
3. If you are using sqlite then you need to write a correct path to sqlite db file
            
            ActiveRecord::Base.establish_connection({
              adapter:  'sqlite3',
              database: '../not_my_database_development'
            })
## ------------------------ ActiveRecord LOCK ------------------------

1. How to lock creating object before running the next query?
```ruby
    with_lock do
      codes.create(generated_attrubutes)
    end
```
