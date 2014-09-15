#angular-resource-tastypie
Simple angularJs client for django-tastypie or equivalent schema RESTful.

##Requirements
- AngularJs

##Usage
controller.js
```javascript
angular.module('myApp', ['ngResourceTastypie'])

.config(function($tastypieProvider){
    $tastypieProvider.setResourceUrl('http://127.0.0.1:8001/api/v1/');
    $tastypieProvider.setAuth('admin','320c4e7da6ed93946f97f51e6f4c8354a098bb6e');
})

.controller('MyCtrl', ['$scope', '$tastypieResource', function($scope, $tastypieResource){

    $scope.Service = new $tastypieResource('service', {limit:5});
    $scope.Service.objects.$find();
    
}]);
```

view.html
```html
...
    <script src="angular.min.js"></script>
    <script src="angular-resource.min.js"></script>
    <script src="angular-resource-tastypie-1.0.min.js"></script>
    <script src="controller.js"></script>
...
```

**Add the module dependency:**
```javascript
angular.module('myApp', ['ngResourceTastypie'])
```

**Add your web service provider configuration:**
```javascript
.config(function($tastypieProvider){
    $tastypieProvider.setResourceUrl('http://127.0.0.1:8001/api/v1/');
    $tastypieProvider.setAuth('admin','320c4e7da6ed93946f97f51e6f4c8354a098bb6e');
})
```

*NOTE*
```javascript
$tastypieProvider.setAuth('username','api_key');
```
<blockquote>
<p>
This api_key was fixed only for demonstration. 
You must generate a dynamic key during the login User, 
in its authorization system, and then configure this attribute. 
With django-tastypie this task is quite simple: 
http://django-tastypie.readthedocs.org/en/latest/authentication.html
</p>
</blockquote>

**Add dependency in the scope:**
```javascript
.controller('MyCtrl', ['$scope', '$tastypieResource', function($scope, $tastypieResource){
    ...
}]);
```

## $tastypieResource
This class is responsible by connect on the specific "list endpoint".
This is where all magic happens.

<h5>Consider the following example:</h5>
We have a service called "song", responsible for providing the "TOP 100 SONGS CLASSIC ROCK".
```
http://127.0.0.1:8001/api/v1/song/
```

