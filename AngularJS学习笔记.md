### Angular versions and their relationships
AngularJS refers to Angular 1.X, which is a javascript open-source front-end library.
Meanwhile Angular is specially targeted at Angular 2.0+, which is an Type-script open-source front-end library.

### IntelliJ configs: 
1. use browser-sync to auto-refresh the dev pages;  
run the command under the dir of your project: `browser-sync start --server --files "**/*"` (watch all the files from your project)  
2. Add angular as external library in Intellij to add more coding assitance such as auto-filling and documentation helper.

### Components

### isolated scope for angular components
Every angularjs component has an isolated scope. It does not access $scope values from **parent elements**, nor does it provide values on $scope for **children components** to access.  
If you want to transfer props from parent to children comps(or vice versa), then you have to use **binding** in config bag;
### Component Router
![](https://docs.angularjs.org/img/guide/component-based-architecture.svg)
