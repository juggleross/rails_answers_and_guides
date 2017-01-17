1. How you can include angular?

        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.1/angular.min.js"></script>
## MODULE

1. How you can define module?
        
        var app =  angular.module("store", [])
2. How you can include angular module?
       
        <html ng-app="store">
        
        </heml>
        
## VIEW

1. How you can show array of object?  
        
        # products it is array
        
        <div ng-repeat="product in products" > 
            <p>{{ product.name }}</p> 
            <p>{{ product.price}}</p> 
            <p>{{ product.pubdate }}</p> 
        </div>
2. How you can include controller to html?
      
        <div ng-controller="MainController">
           ...
        </div>
3. How you can add image?
        
        <img ng-src="{{ product.cover }}">
        
4. How you can know index when we use ng-repeat?
        
        $index
5. How you can run function on click?
        
        <div ng-click="plusOne($index)">
            ...
        </div>
6. How you can set value by click?
        
        <a href="" ng-click="tab = 1"> ... </a>
        {{ tab }} 
        
        # tab => 1
6. How you can init value ?
        
        <div ng-init="tab = 1"> ... </div>
        
6. How you can show tag when attribute is true?
        
        <button ng-show="true"> ... </button>
7. How you can hide tag when attribute is true?
        
        <button ng-hide="true"> ... </button>
8. How you can cpecify class?
        
        <li ng-class="{ active: true }"> .. </li>

## CONTROLLER

1. Can you show me example of angular simple controller?
    
               app.controller('MainController', ['$scope', function($scope) { 
                  $scope.title = 'Top Sellers in Books my';
                  $scope.promo = "My promo";
                  $scope.product = {
                    name: "The Book of Trees",
                    price: 19,
                    pubdate: new Date('2014', '03', '08')
                  };
                }]);

        
3. How you can get array of object into controller?
    
                 $scope.product = [ 
                      { 
                        name: 'The Book of Trees', 
                        price: 19, 
                        pubdate: new Date('2014', '03', '08'), 
                        cover: 'img/the-book-of-trees.jpg' 
                      }, 
                      { 
                        name: 'Program or be Programmed', 
                        price: 8, 
                        pubdate: new Date('2013', '08', '01'), 
                        cover: 'img/program-or-be-programmed.jpg' 
                      } 
                    ]
3. Hoy you can define function into controller?
      
               $scope.plusOne = function(index) { 
                    $scope.products[index].likes += 1; 
                };


## FILTER

1. What filter can convert integer to MONEY?
      
        {{ product.price | currency}}
2. What filter you will be use for DATE?
        
        {{ product.pubdate | date }}
3. UPPERCASE?
        
        {{ product.name | uppercase}}
4. How you can limit ng-repeat count in array?
        
        < div ng-repeat="product in products | limitTo:3"> ... </div>
5. How you can ordered array?
        
         < div ng-repeat="product in products | orderedBy:'-price'"> ... </div>
        
        
## DIRECTIVE

1. How you can specify new directive(tag) ?
        
        # appinfo.js
                app.directive('appInfo', function() { 
                  return { 
                    restrict: 'E', 
                    scope: { 
                      info: '=' 
                    }, 
                    templateUrl: 'js/directives/appInfo.html' 
                  }; 
                });

        # appInfo.html
                <img class="icon" ng-src="{{ info.icon }}"> 
                <h2 class="title">{{ info.title }}</h2> 
                <p class="developer">{{ info.developer }}</p> 
        
        # index.html
                <app-info info="move"></app-info>
## SERVICE

1. How you can define service?
        
        # service.js
                app.factory('forecast', ['$http', function($http) { 
                  return $http.get('https://s3.amazonaws.com/codecademy-content/courses/ltp4/forecast-api/forecast.json') 
                            .success(function(data) { 
                              return data; 
                            }) 
                            .error(function(err) { 
                              return err; 
                            }); 
                }]);
        
        # inside controller
                app.controller('MainController', ['$scope', 'forecast', function($scope, forecast) { 
                  forecast.success(function(data) { 
                    $scope.fiveDay = data; 
                  });
                }]);
                
## ROYTING

1. How you can define simple route?
        
        # inside app.js
        
        var app = angular.module('GalleryApp', ['ngRoute']);
        app.config(function ($routeProvider) { 
          $routeProvider 
            .when('/', { 
              controller: 'HomeController', 
              templateUrl: 'views/home.html' 
            })
            .when('/photos/:id',{
              controller: 'PhotoController', 
              templateUrl: 'views/photo.html' 
            })
            .otherwise({ 
              redirectTo: '/' 
            }); 
        });
