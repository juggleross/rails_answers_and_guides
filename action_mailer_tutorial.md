1. How to see a successful message without a real delivery? letter_oppener
```ruby
# First add the gem to your development environment and run the bundle command to install it.
    gem "letter_opener", :group => :development
# Then set the delivery method in config/environments/development.rb
    config.action_mailer.delivery_method = :letter_opener
```
___
2. How to create simple ActionMailer? 
      
            # app/mailers/user_mailer.rb
            class UserMailer < ApplicationMailer
              default from: 'notifications@example.com'

              def welcome_email(user)
                @user = user
                @url  = 'http://example.com/login'
                mail(to: @user.email, subject: 'Welcome to My Awesome Site')
              end

            end

            # welcome_email.html.erb в app/views/user_mailer/
            <!DOCTYPE html>
            <html>
              <head>
                <meta content='text/html; charset=UTF-8' http-equiv='Content-Type' />
              </head>
              <body>
                <h1>Welcome to example.com, <%= @user.name %></h1>
                <p>
                  You have successfully signed up to example.com,
                  your username is: <%= @user.login %>.<br>
                </p>
                <p>
                  To login to the site, just follow this link: <%= @url %>.
                </p>
                <p>Thanks for joining and have a great day!</p>
              </body>
            </html>

            # add somewhere in controller
            UserMailer.welcome_email(@user).deliver_later
3. Good article about testing actionMailer and rspec?
            
            https://blog.lucascaton.com.br/index.php/2010/10/25/how-to-test-mailers-in-rails-3-with-rspec/
4. How to generate random password with devise?
            
            generated_password = Devise.friendly_token.first(8)
            user = User.create!(:email => email, :password => generated_password)
5. Send random password after callback?
            
              before_validation :set_password, on: :create
              after_create :send_email

              private

              def set_password
                temp_password = Devise.friendly_token.first(8)
                if self.password.nil? && !self.email.nil?
                  self.password = temp_password
                  self.password_confirmation = temp_password
                end
              end

              def send_email
                UserMailer.welcome_email(self, self.password).deliver_later
              end
6. How to generate mailer?
            
             rails generate mailer User
7. What method you know for deliver letter?
            
            UserMailer.welcome_email(self, self.password).deliver_now
              and
            UserMailer.welcome_email(self, self.password).deliver_later
 
8. How you can test deliver_letter method?
            
            # add active job and perform_enqueued_jobs
            include ActiveJob::TestHelper
            
            it 'sends email with coupon code to user' do
              expect do
                perform_enqueued_jobs do
                  described_class.new(user).call
                end
              end.to change { UserMailer.deliveries.count }.by(1)
            end
            
9. How to create link for account activation?
            
              = link_to "activate", edit_account_activation_url(@user.activation_token, email: @user.email)
10. Set default url for email
            
            config.action_mailer.default_url_options = { host: "localhost:3000" }
