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
component router is decrapted for 1.6.5, replace it with ngRoute or ui-router. 
$location in HTML5 mode requires a <base> tag to be present!
![](https://docs.angularjs.org/img/guide/component-based-architecture.svg)


#### ui-router
* ui-sref
>A **ui-sref** is a directive, and behaves similar to an html href. Instead of referencing a url like an href, it references a state. **The ui-sref directive automatically builds a href attribute for you (<a href=...></a>) based on your state’s url.**

该项解答了ui-sref directive可以与href混合使用的现象（当然不能作用于同一标签，但可以作用于比如有两个不同的<a>tag）  

* nested states
>When naming a state, prepending another state’s name (and a dot) creates a parent/child relationship. In this case, the people.person state is **a child** of the people state.
>Another way to create a parent/child relationship is with the parent: property of a state definition.

第二种方法申明`state: parent: state variable name`
 ```javascript
 var programmeState = {
            name: 'Programme',
            url: '/programme',
            abstract: true,
            component: 'programme'
        };
        var progAbtState = {
            name: 'about',
            url: '#about'
            //parent: 'programmeState'
        };
  ```
  生成的url为 /programme#about;  
We can also mix nested states with state parameters: 
```javascript
.config(function($stateProvider) {
        var programmeState = {
            name: 'Programme',
            url: '/programme',
            abstract: true,
            component: 'programme'
        };
        //children states for programmeState;
        var dropdownState = {
            name: 'Programme.dropdown',
            url: '#{dropdownName}'
        };
        ```
在view上应用parameters:
```html
<ul class="dropdown-menu dropdown-restyle" aria-labelledby="{{pane.name}}Dropdown"  ng-show="pane.dropdowns!=null">
                <li ng-repeat="dropdown in pane.dropdowns">
                    <!--<a href="javascript:; " ng-click="$ctrl.scrollToId(dropdown)">{{dropdown}}</a>-->
                    <a ui-sref="Programme.dropdown({dropdownName: dropdown.toLowerCase() })">{{dropdown}}</a>
                </li>
            </ul>
            ```
