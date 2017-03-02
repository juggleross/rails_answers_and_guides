1. How to add language with help object?
      
      	var fruits = {
            APPLE: 'Apple'
            CITRIC: {
                ORANGE: 'Orange' 
            }
        };

        $translateProvider
        .translations('en', fruits)
        .preferredLanguage('en');
        
2. How you can set default language?
        
        $translateProvider.preferredLanguage('ru');
3. How you can use interpolition variable?
        
            {
              "DELICIOUS_FRUIT": "{{fruit_name}} is delicious!"
            }
            
            {{ 'DELICIOUS_FRUIT' | translate:'{ fruit_name: “Apple” }' }}
4. How you can set automaticaly determination language?
            
            // try to find out preferred language by yourself
            $translateProvider.determinePreferredLanguage();
5. How to add button for changing language?
            
            <button ng-click="changeLanguage('de')" translate="BUTTON_LANG_DE"></button>
            <button ng-click="changeLanguage('en')" translate="BUTTON_LANG_EN"></button>
            
            app.controller('Ctrl', ['$translate', '$scope', function ($translate, $scope) {
 
              $scope.changeLanguage = function (langKey) {
                $translate.use(langKey);
              };
            }]);