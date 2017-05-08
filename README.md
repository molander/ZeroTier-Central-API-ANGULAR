# Getting started

## How to Build

The generated SDK requires AngularJS framework to work. If you do not already have angular downloaded, please go ahead and do it from [here](https://angularjs.org/).
If any of your models have `Date` or `Datetime` type fields or your endpoints have `Date`/`Datetime` type response, you will need to download and link [angular-moment](https://cdnjs.cloudflare.com/ajax/libs/angular-moment/1.0.1/angular-moment.min.js) and [moment.js](https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.17.1/moment.min.js) with your project.

## How to Use

The following section describes how to use the generated SDK in an existing/new project.

### 1. Configure Angular and Generated SDK
Perform the following steps to configure angular and the SDK:
+ Make a `scripts` folder inside the root folder of the project. If you already have a `scripts` folder, skip to the next step.
+ Move the `angular.min.js` file inside the scripts folder. 
+ Move the `zerotiercentralapilib` folder inside the scripts folder.
+ If any of the Custom Types in your API have `Date`/`Datetime` type fields or any endpoint has `Date`/`Datetime` response, you will need to download angular-moment and moment.js. Move these 2 files into the `scripts` folder as well.

![folder-structure-image](https://apidocs.io/illustration/angularjs?step=folderStructure&workspaceFolder=ZeroTier%20Central%20API-Angular&projectName=ZeroTierCentralAPILib)

### 2. Open Project Folder
Open an IDE/Text Editor for JavaScript like Sublime Text. The basic workflow presented here is also applicable if you prefer using a different editor or IDE.  
Click on `File` and select `Open Folder`

Select the folder of your SDK and click on `Select Folder` to open it up in Sublime Text. The folder will become visible in the bar on the left.

![open-folder-image](https://apidocs.io/illustration/angularjs?step=openFolder&workspaceFolder=ZeroTier%20Central%20API-Angular)

### 3. Create an Angular Application
Since Angular JS is used for client-side web development, in order to use the generated library, you will have to develop an application first.
If you already have an angular application, [skip to Step 6](#6-include-sdk-references-in-html-file). Otherwise, follow these steps to create one:

+ In the IDE, click on `File` and choose `New File` to create a new file.
+ Add the following starting code in the file:
```js
    var app = angular.module('myApp', []);
    app.controller('testController', function($scope) 
    {

    });
```
+ Save it with the name `app.js` in the `scripts` folder.


### 4. Create HTML File
Skip to the next step if you are working with an existing project and already have an html file. Otherwise follow the steps to create one:
+ Inside the IDE, right click on the project folder name and select the `New File` option to create a new test file.
+ Save it with an appropriate name such as `index.html` in the root of your project folder.
`index.html` should look like this:
```html
	<!DOCTYPE html>
	<html>
	<head>
		<title>Angular Project</title>
		<script></script>
	</head>

	<body>
	</body>

	</html>
```

![initial-html-code-image](https://apidocs.io/illustration/angularjs?step=initialCode&workspaceFolder=ZeroTier%20Central%20API-Angular)

### 5. Including links to Angular in HTML file
Your HTML file needs to have a link to `angular.min.js` file to use Angular-JS. Add the link using `script` tags inside the `head` section of `index.html` like:
```html
	<script src="scripts/angular.min.js" ></script>
```
If any of the Custom Types that you have defined have `Date`/`Datetime` type fields or any endpoint has `Date`/`Datetime` response, you will also need to link to angular-moment and moment.js like:
```html
	<script src="scripts/angular.min.js" ></script>
	<script src="scripts/moment.min.js" ></script>
	<script src="scripts/angular-moment.min.js" ></script>
```

### 6. Include SDK references in HTML file
Import the reference to the generated SDK files inside your html file like:
```html
	<head>
		...
		<!-- Helper files -->
		<script src="scripts/zerotiercentralapilib/Module.js"></script>
		<script src="scripts/zerotiercentralapilib/Configuration.js"></script>
		<script src="scripts/zerotiercentralapilib/APIHelper.js"></script>
		<script src="scripts/zerotiercentralapilib/Http/Client/HttpContext.js"></script>
		<script src="scripts/zerotiercentralapilib/Http/Client/RequestClient.js"></script>
		<script src="scripts/zerotiercentralapilib/Http/Request/HttpRequest.js"></script>
		<script src="scripts/zerotiercentralapilib/Http/Response/HttpResponse.js"></script>

		<!-- API Controllers -->
        <script src="scripts/zerotiercentralapilib/Controllers/GeneralQueriesController.js"></script>
        <script src="scripts/zerotiercentralapilib/Controllers/UserController.js"></script>
        <script src="scripts/zerotiercentralapilib/Controllers/NetworkController.js"></script>
        <script src="scripts/zerotiercentralapilib/Controllers/MemberController.js"></script>


		<!-- Models -->
        <script src="scripts/zerotiercentralapilib/Models/BaseModel.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/Status.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/RandomToken.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/User.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/GlobalPermissions.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/Permissions.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/MId.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/Network.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/Config.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/Member.js"></script>
        <script src="scripts/zerotiercentralapilib/Models/Config11.js"></script>

		...
	</head>
```
> The `Module.js` file should be imported before the other files. After `Module.js`, `Configuration.js` should be imported.

### 7. Including link to `app.js` in HTML file
Link your `app.js` file to your `index.html` file like:
```html
	<head>
		...
		<script src="scripts/app.js"></script>
	</head>
```
> The link to app.js needs to be included at the very end of the head tag, after the SDK references have been added

### 8. Initializing the Angular App
You need to initialize your app and the controller associated with your view inside your `index.html` file. Do so like:
+ Add ng-app directive to initialize your app inside the `body` tag.
```html
	<body ng-app="myApp">
```
+ Add ng-controller directive to initialize your controller and bind it with your view (`index.html` file).
```html
	...
	<body ng-app="myApp">
		<div ng-controller="testController">
			...
		</div>
		...
	</body>
	...
```

### 9. Consuming the SDK 
In order to use the generated SDK's modules, controllers and factories, the project needs to be added as a dependency in your angular app's module. This will be done inside the `app.js` file.
Add the dependency like this:

```js
    var app = angular.module('myApp', ['ZeroTierCentralAPILib']);
```
At this point, the SDK has been successfully included in your project. Further steps include using a service/factory from the generated SDK. To see working example of this, please head on [over here](#list-of-controllers) and choose any class to see its functions and example usage.  

### 10. Running The App
To run the app, simply open up the `index.html` file in a browser.

![app-running](https://apidocs.io/illustration/angularjs?step=appRunning)

## Initialization

### Authentication
In order to setup authentication and initialization of the Angular App, you need the following information.

| Parameter | Description |
|-----------|-------------|
| basicAuthUserName | The username to use with basic authentication |
| basicAuthPassword | The password to use with basic authentication |



```JavaScript
// Configuration parameters and credentials
basicAuthUserName = "basicAuthUserName"; // The username to use with basic authentication
basicAuthPassword = "basicAuthPassword"; // The password to use with basic authentication

```
The Angular App can be initialized as following:
```html
<body ng-app="myApp">
    <div ng-controller="testController">
        ...
    </div>
    ...
</body>
```
> The initialization code will be added inside the `index.html` file (which is the view of the app you have created). More detail about this can be found in the [`How to Use`](#how-to-use) section

# Class Reference

## <a name="list_of_controllers"></a>List of Controllers

* [GeneralQueriesController](#general_queries_controller)
* [UserController](#user_controller)
* [NetworkController](#network_controller)
* [MemberController](#member_controller)

## <a name="general_queries_controller"></a>![Class: ](https://apidocs.io/img/class.png ".GeneralQueriesController") GeneralQueriesController

### Get singleton instance

The singleton instance of the ``` GeneralQueriesController ``` class can be accessed via Dependency Injection.

```js
	app.controller("testController", function($scope, GeneralQueriesController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	});
```

### <a name="get_status_and_configuration_information"></a>![Method: ](https://apidocs.io/img/method.png ".GeneralQueriesController.getStatusAndConfigurationInformation") getStatusAndConfigurationInformation

> Get Status and Configuration Information


```javascript
function getStatusAndConfigurationInformation()
```

#### Example Usage

```javascript


	app.controller("testController", function($scope, GeneralQueriesController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	

		var result = GeneralQueriesController.getStatusAndConfigurationInformation();
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="get_currently_authenticated_user"></a>![Method: ](https://apidocs.io/img/method.png ".GeneralQueriesController.getCurrentlyAuthenticatedUser") getCurrentlyAuthenticatedUser

> Get Currently Authenticated User


```javascript
function getCurrentlyAuthenticatedUser()
```

#### Example Usage

```javascript


	app.controller("testController", function($scope, GeneralQueriesController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	

		var result = GeneralQueriesController.getCurrentlyAuthenticatedUser();
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="get_generate_a_random_token"></a>![Method: ](https://apidocs.io/img/method.png ".GeneralQueriesController.getGenerateARandomToken") getGenerateARandomToken

> Generate a Random Token


```javascript
function getGenerateARandomToken()
```

#### Example Usage

```javascript


	app.controller("testController", function($scope, GeneralQueriesController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	

		var result = GeneralQueriesController.getGenerateARandomToken();
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="create_terminate_current_session"></a>![Method: ](https://apidocs.io/img/method.png ".GeneralQueriesController.createTerminateCurrentSession") createTerminateCurrentSession

> Terminate Current Session


```javascript
function createTerminateCurrentSession()
```

#### Example Usage

```javascript


	app.controller("testController", function($scope, GeneralQueriesController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	

		var result = GeneralQueriesController.createTerminateCurrentSession();
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



[Back to List of Controllers](#list_of_controllers)

## <a name="user_controller"></a>![Class: ](https://apidocs.io/img/class.png ".UserController") UserController

### Get singleton instance

The singleton instance of the ``` UserController ``` class can be accessed via Dependency Injection.

```js
	app.controller("testController", function($scope, UserController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	});
```

### <a name="retrieve_a_user"></a>![Method: ](https://apidocs.io/img/method.png ".UserController.retrieveAUser") retrieveAUser

> Retrieve a User


```javascript
function retrieveAUser(userId)
```
#### Parameters

| Parameter | Tags | Description |
|-----------|------|-------------|
| userId |  ``` Required ```  | 0000-0000-0000-000000000000 (required,string) - Internal user ID (GUID) |



#### Example Usage

```javascript


	app.controller("testController", function($scope, UserController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	    var userId = "00000000";


		var result = UserController.retrieveAUser(userId);
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="update_a_user"></a>![Method: ](https://apidocs.io/img/method.png ".UserController.updateAUser") updateAUser

> Update a User


```javascript
function updateAUser(userId)
```
#### Parameters

| Parameter | Tags | Description |
|-----------|------|-------------|
| userId |  ``` Required ```  | 0000-0000-0000-000000000000 (required,string) - Internal user ID (GUID) |



#### Example Usage

```javascript


	app.controller("testController", function($scope, UserController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	    var userId = "00000000";


		var result = UserController.updateAUser(userId);
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="get_all_viewable_users"></a>![Method: ](https://apidocs.io/img/method.png ".UserController.getAllViewableUsers") getAllViewableUsers

> Get All Viewable Users


```javascript
function getAllViewableUsers()
```

#### Example Usage

```javascript


	app.controller("testController", function($scope, UserController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	

		var result = UserController.getAllViewableUsers();
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



[Back to List of Controllers](#list_of_controllers)

## <a name="network_controller"></a>![Class: ](https://apidocs.io/img/class.png ".NetworkController") NetworkController

### Get singleton instance

The singleton instance of the ``` NetworkController ``` class can be accessed via Dependency Injection.

```js
	app.controller("testController", function($scope, NetworkController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	});
```

### <a name="retrieve_a_network"></a>![Method: ](https://apidocs.io/img/method.png ".NetworkController.retrieveANetwork") retrieveANetwork

> Retrieve a Network


```javascript
function retrieveANetwork(networkId)
```
#### Parameters

| Parameter | Tags | Description |
|-----------|------|-------------|
| networkId |  ``` Required ```  | 16-digit ZeroTier network ID |



#### Example Usage

```javascript


	app.controller("testController", function($scope, NetworkController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	    var networkId = "0000000000000000";


		var result = NetworkController.retrieveANetwork(networkId);
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="update_or_create_a_network"></a>![Method: ](https://apidocs.io/img/method.png ".NetworkController.updateOrCreateANetwork") updateOrCreateANetwork

> Update or create a Network


```javascript
function updateOrCreateANetwork(networkId, body)
```
#### Parameters

| Parameter | Tags | Description |
|-----------|------|-------------|
| networkId |  ``` Required ```  | 16-digit ZeroTier network ID |
| body |  ``` Required ```  | TODO: Add a parameter description |



#### Example Usage

```javascript


	app.controller("testController", function($scope, NetworkController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	    var networkId = "0000000000000000";
    var body = new Network({  "id": "",  "type": "",  "clock": 0,  "ui": {},  "rulesSource": "",  "description": "",  "permissions": {    "{id}": {      "r": false,      "m": false,      "d": false,      "a": false,      "o": false,      "t": ""    }  },  "onlineMemberCount": 0,  "capabilitiesByName": {},  "tagsByName": {},  "circuitTestEvery": 0,  "config": {    "id": "",    "nwid": "",    "name": "",    "objtype": "",    "private": false,    "creationTime": 0,    "revision": 0,    "lastModified": 0,    "multicastLimit": 0,    "routes": [],    "rules": [],    "tags": [],    "capabilities": [],    "totalMemberCount": 0,    "activeMemberCount": 0,    "authTokens": [],    "authorizedMemberCount": 0,    "v4AssignMode": {},    "v6AssignMode": {}  }});


		var result = NetworkController.updateOrCreateANetwork(networkId, body);
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="delete_a_network"></a>![Method: ](https://apidocs.io/img/method.png ".NetworkController.deleteANetwork") deleteANetwork

> Delete a Network


```javascript
function deleteANetwork(networkId)
```
#### Parameters

| Parameter | Tags | Description |
|-----------|------|-------------|
| networkId |  ``` Required ```  | 16-digit ZeroTier network ID |



#### Example Usage

```javascript


	app.controller("testController", function($scope, NetworkController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	    var networkId = "0000000000000000";


		var result = NetworkController.deleteANetwork(networkId);
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="get_all_viewable_networks"></a>![Method: ](https://apidocs.io/img/method.png ".NetworkController.getAllViewableNetworks") getAllViewableNetworks

> Get All Viewable Networks


```javascript
function getAllViewableNetworks()
```

#### Example Usage

```javascript


	app.controller("testController", function($scope, NetworkController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	

		var result = NetworkController.getAllViewableNetworks();
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



[Back to List of Controllers](#list_of_controllers)

## <a name="member_controller"></a>![Class: ](https://apidocs.io/img/class.png ".MemberController") MemberController

### Get singleton instance

The singleton instance of the ``` MemberController ``` class can be accessed via Dependency Injection.

```js
	app.controller("testController", function($scope, MemberController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	});
```

### <a name="retrieve_a_member"></a>![Method: ](https://apidocs.io/img/method.png ".MemberController.retrieveAMember") retrieveAMember

> Retrieve a Member


```javascript
function retrieveAMember(networkId, nodeId)
```
#### Parameters

| Parameter | Tags | Description |
|-----------|------|-------------|
| networkId |  ``` Required ```  | 16-digit ZeroTier network ID |
| nodeId |  ``` Required ```  | 10-digit ZeroTier node ID (a.k.a. ZeroTier address) |



#### Example Usage

```javascript


	app.controller("testController", function($scope, MemberController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	    var networkId = "networkId";
    var nodeId = "nodeId";


		var result = MemberController.retrieveAMember(networkId, nodeId);
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



### <a name="update_or_add_a_member"></a>![Method: ](https://apidocs.io/img/method.png ".MemberController.updateOrAddAMember") updateOrAddAMember

> Update or add a Member


```javascript
function updateOrAddAMember(networkId, nodeId, body)
```
#### Parameters

| Parameter | Tags | Description |
|-----------|------|-------------|
| networkId |  ``` Required ```  | 16-digit ZeroTier network ID |
| nodeId |  ``` Required ```  | 10-digit ZeroTier node ID (a.k.a. ZeroTier address) |
| body |  ``` Required ```  | TODO: Add a parameter description |



#### Example Usage

```javascript


	app.controller("testController", function($scope, MemberController,Status,RandomToken,User,GlobalPermissions,Permissions,MId,Network,Config,Member,Config11){
	    var networkId = "networkId";
    var nodeId = "nodeId";
    var body = new Member({"key":"value"});


		var result = MemberController.updateOrAddAMember(networkId, nodeId, body);
        //Function call returns a promise
        result.then(function(success){
			//success case
			//getting context of response
			console.log(success.getContext());
		},function(err){
			//failure case
		});

	});
```



[Back to List of Controllers](#list_of_controllers)



