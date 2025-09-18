### Create Angular project without Node.js
```html
<html>
<head>
  <title>Angular with node.js</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.8.3/angular.min.js"></script>
</head>

<body>
  <div ng-app>
    <h1>Hello Angular</h1>
    <p>Sum of 20 and 10 is {{20+10}}</p>
    <p>My first name is {{{ name:'Anurag', age: '23'}.name}}</p>
    <p>Printing array: {{['ABC', 'DEF', 'GHI'][2]}}</p>
  </div>
</body>

</html>
```


## Create Angular project with Node.js

___Steps to create Angular Project__
1. Check Node and NPM version installed in you system.
2. Install the CLI for Angular -> `npm intall -g @angular/cli@latest`
3. Check angular is installed ng-version: `ng version`,  `ng --v`or `ng -version`.
4. Use ng version
5. Create a folder where angular project will be saved and enter the folder and execute the command: 
	`ng new <directory_name>`
	or
	`ng new <project-name> --dry-run`
6. Start the project with command `ng serve`.


