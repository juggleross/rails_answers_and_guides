1. Articles
      
        http://guides.rubyonrails.org/engines.html
2. How to create own engine?
      
        rails plugin new blorgh --mountable
3. Hot to add your existing engine to your app?
        
        # path to your engines from current app
            gem 'blorgh', path: 'engines/blorgh'
        
        # config/routes.rb
            mount Blorgh::Engine, at: "/blog"  
        
        # then add migrations
            rails blorgh:install:migrations