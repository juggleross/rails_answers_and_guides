1. How you can start sinatra?
        
        require 'sinatra' 
        get '/' do 
          "Just Do It" 
        end
2. How you can stop sinatra server?
        
        ctr + c
        # if it already late write fg (foreground)
3. Where you have to store .slim files?
        
        into views folder 
4. What sign use to evaluate a Ruby variable in slim?

        = @rub_variable
5. Example of dinamic content in sinatra (take params)
        
        get '/:task' do
          @task = params[:task]
          slim :task
        end
6. Example of form for post request in slim 
        
        form action="/" method="POST"
            input type="text" name="task"
            input.button type="submit" value="New Task >>"
        
        post '/' do
          slim :example_above
        end
7. How you can call erb file?
        
        get '/' do
          erb :index
        end
8.  Example of form for post request in erb
        
        <form action='cast' method='post'>
                <% Choices.each do |id, text| %>
                      <input type='radio' name='vote' value='<%= id %>' id='vote_<%= id %>' />
                      <%= text %>
                <% end %>
              <button type='submit' class='btn btn-primary'>Cast this vote!</button>
         </form>
9. How you can add bootstrap file to sinatra?
        
        - create folder 'public'
        - inside 'public' create folder 'vendor'
        - add all bootstrap file there
        - include bootstrap <link href="/vendor/bootstrap/css/bootstrap.min.css" rel="stylesheet">
10. How you can set start value in sinatra?
        
        configure do
          set :foo, 'bar'
        end

        get '/' do
          settings.foo? # => true
          settings.foo  # => 'bar'
        end
11. How you can set true and false value?
        
        enable  :sessions, :logging #=> true
        disable :dump_errors, :some_custom_option #=> false
12. How you can define method?
        
        # with help helpers
        helpers do
          def bar(name)
            "#{name}bar"
          end
        end

        get '/:name' do
          bar(params['name'])
        end
 13. How you can use sessions?
        
         enable :sessions
         
         get '/' do
           "value = " << session[:value].inspect
         end

         get '/:value' do
           session['value'] = params['value']
         end
14. How you can immediately stop request?

        halt 'this will be the body'
        halt 410
15. How you can use pattern in request? 
        
        get '/say/*/to/*' do
          # matches /say/hello/to/world
          params['splat'] # => ["hello", "world"]
        end

        get '/download/*.*' do
          # matches /download/path/to/file.xml
          params['splat'] # => ["path/to/file", "xml"]
        end
16. How you can take params from input tag?
        
        # inside form  tag
        <input type="text" name='word'>
        # inside post method
        @word = params['word']
        

