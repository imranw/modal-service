# modal-service
Ionic modal wrapper that return a result after closing modal

More practical way to create and display modals with some features below:

- Pass parameters;
- Set an independent controller;
- Isolate the scope of the modal;
- Get results after completing / close the modal;
- Use promises to get the result;

#Link module in your HTML

```html
<script src="[path]/modal-service.js"></script>
```

#Add module on your angular app
```javascript
angular.module('myApp', ['modalService']);
```

#Use service
You can assign an indipendent controller to the modal, a specific html view and an input param.
In controller is possible to obtain the parameters injecting `parameters` and close modal passing the result in `closeModal(result)` method.

```javascript
angular.module('myApp')

.controller('ExampleCtrl', function($scope, $modalService){

    //Open modal and attend resutl
    $modalService.show('modals/example-modal.html', 'ClubSelectionCtrl', {name: 'Valerio Barbera', city: 'Naples'})
        .then(function(result){
            if(!result)
                alert('Club is not selected');
            else{
                $scope.club = result;
                console.log($scope.club);
            }
        });

})

.controller('ClubSelectionCtrl', function($scope, parametes){
    
    //This is the JSON input parameter forwarded into $modalService.show(...)
    console.log(parameters);
    
    $scope.name = parameters.name;
    
    $scope.clubs = [
        { id: 1, name: "Real Madrid"},
        { id: 2, name: "Milan"},
        { id: 3, name: "Porto"},
    ];
    
    $scope.select = function(club){
        $scope.closeModal(club);
    };
});
```

#Your modal template

```html
<div class="modal">

    <ion-header-bar class="bar bar-header bar-light">
        <button class="button button-clear" ng-click="closeModal(null)"><i class="icon ion-ios-arrow-back"></i></button>
    </ion-header-bar>
    
    <ion-content padding="true">
        <ion-list>
            <ion-item ng-repeat="club in clubs" ng-click="selectClub(club)">
                {{club.name}}
            </ion-item>
        </ion-list>
    </ion-conten>
</div>
```
