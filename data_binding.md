
# Data Binding
For two way binding data between view and model. JQM refers to `$()` or `append`. 
**JQM:**

*index.html:*
```html
   <h1 id="fruit-topic"></h1>
   <h2 id="fruit-subtopic"></h2>
   
      <ul id ="fruit-list">
         
      </ul>
      <p>There are many more!</p>
```

*index.js:*
```js
      $( document ).ready(function() {
         var title = "My favourite Fruit";
         var fruit = ["Durian", "Apple", "Orange", "Watermelon", "Grape"];
         var subtitle = "My top favourite fruit is " + fruit[0] + "!";
         $('#fruit-topic').append(title);
         $('#fruit-subtopic').append(subtitle);
         $('#fruit-list').append("<li>" + fruit[0] + "</li>" + 
                                 "<li>" + fruit[1] + "</li>" +
                                 "<li>" + fruit[2] + "</li>" +
                                 "<li>" + fruit[3] + "</li>" +
                                 "<li>" + fruit[4] + "</li>");
      });

```

**Ionic:**

*home.html:*
```html
<ion-content>
   <h1>{{title}}</h1>
   <h2>My top favourite is {{favFruit}}!</h2>
   
      <ul>
      <li>{{fruits[0]}}</li>
      <li>{{fruits[1]}}</li>
      <li>{{fruits[2]}}</li>
      <li>{{fruits[3]}}</li>
      <li>{{fruits[4]}}</li>
      </ul>
      <p>There are many more!</p>
   
</ion-content>
```

*home.ts*
 ```ts
import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {
// add this
title = 'My Favourite Fruit';
fruits = ['Durian', 'Apple', 'Orange', 'Watermelon', 'Grape'];
favFruit = this.fruits[0];

  constructor(public navCtrl: NavController) {

  }
 . . . 
 
}
 ```


### ngFor
ngFor is a method to loop through your data in app view. JQM will refer as `for loop`.

**JQM:**

*index.html:*
```html
   <h1 id="fruit-topic"></h1>
   <h2 id="fruit-subtopic"></h2>
   
      <ul id ="fruit-list">
         
      </ul>
      <p>There are many more!</p>
```

*index.js:*
```js
      $( document ).ready(function() {
         var title = "My favourite Fruit";
         var fruit = ["Durian", "Apple", "Orange", "Watermelon", "Grape"];
         var subtitle = "My top favourite fruit is " + fruit[0] + "!";
         $('#fruit-topic').append(title);
         $('#fruit-subtopic').append(subtitle);
         for(var i = 0; i< fruit.length; i++){
            $('#fruit-list').append("<li>" + fruit[i] + "</li>");
         }
      });

```

**Ionic:**
```html
<ion-content>
   <h1>{{title}}</h1>
   <h2>My top favourite is {{favFruit}}!</h2>
   
      <ul>
      <li>{{fruits[0]}}</li>
      <li>{{fruits[1]}}</li>
      <li>{{fruits[2]}}</li>
      <li>{{fruits[3]}}</li>
      <li>{{fruits[4]}}</li>
      </ul>
      <p>There are many more!</p>
   
</ion-content>
```

Edit it to:
```html
<ion-content>
   <h1>{{title}}</h1>
   <h2>My top favourite is {{favFruit}}!</h2>
   
      <ul>
      <li *ngFor="let fruit of fruits">
      {{fruit}}
      </li>
      </ul>
      <p>There are many more!</p>
   
</ion-content>
```

### ngIf
ngIf is a method to display a view or a portion of a view only under specific circumstances. JQM refer as `if else statement`.

**JQM:**

*index.html:*
```html
   <h1 id="fruit-topic"></h1>
   <h2 id="fruit-subtopic"></h2>
   
      <ul id ="fruit-list">
         
      </ul>
      <p id="fruit-paragraph"></p>
```

*index.js:*
```js
      $( document ).ready(function() {
         var title = "My favourite Fruit";
         var fruit = ["Durian", "Apple", "Orange", "Watermelon", "Grape"];
         var subtitle = "My top favourite fruit is " + fruit[0] + "!";
         $('#fruit-topic').append(title);
         $('#fruit-subtopic').append(subtitle);
         for(var i = 0; i< fruit.length; i++){
            $('#fruit-list').append("<li>" + fruit[i] + "</li>");
         }

         if(fruit.length>3){
         $('#fruit-paragraph').append("There are many more!");  
         }
      });
```
   
**Ionic:**
```html
<ion-content>
   <h1>{{title}}</h1>
   <h2>My top favourite is {{favFruit}}!</h2>

      <ul>
      <li *ngFor="let fruit of fruits">
      {{fruit}}
      </li>
      </ul>
      <p *ngIf="fruits.length > 3" >There are many more!</p>

</ion-content>
```
*This tells the view to display the paragraph if there more than 3 items in the fruits array data.*



[Angular data binding docs](https://angular.io/guide/displaying-data)

## ngModel
Ngmodel is use for one way data binding from controller to model of an app. JQM refer as `$().value` of other method to get data from the app view.

**JQM:**

*index.html:*
```html
<label for="text-basic">Username:</label>
<input name="text-basic" id="text-basic" value="someUsername" type="text">

<label for="password">Password:</label>
<input name="password" id="password" value="somePassword" type="password">

<label for="textarea-1">Textarea:</label>
<textarea name="textarea-1" id="textarea">someTextArea</textarea>

<label for="textarea-1">Unit:</label>
<select name="select-native-15" id="select">
    <option value="1">Pack</option>
    <option value="2">Bottle</option>
    <option value="3">Piece</option>
</select>
```

*index.js:*
```js
      $( document ).ready(function() {
        var username = $('#text-basic').val(); 
        var password = $('#password').val(); 
        var textArea = $('#textarea').val(); 
        var unit = $('#select').val(); 

        console.log(username); //someUsername
        console.log(password); //somePassword
        console.log(textArea); //someTextArea
        console.log(select); //1
      });
```

**Ionic:**

*home.html:*
```html
     <ion-label>Username:</ion-label>
    <ion-input type="text" [ngModel]="username">someUsername</ion-input>
    
    <ion-label>Password:</ion-label>
    <ion-input type="password" [ngModel]="password">somePassword</ion-input>

    <ion-label>Textarea:</ion-label>
    <ion-textarea type="text"  [ngModel]="textarea"></ion-textarea>
  
    <ion-label>Unit:</ion-label>
    <ion-select [ngModel]="unit">
      <ion-option value="1">Piece(s)</ion-option>
      <ion-option value="2">Pack(s)</ion-option>
      <ion-option value="3">Bottle(s)</ion-option>
    </ion-select>
```

*home.ts*
```ts
import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {
// add this
title = 'My Favourite Fruit';
fruits = ['Durian', 'Apple', 'Orange', 'Watermelon', 'Grape'];
favFruit = this.fruits[0];

  constructor(public navCtrl: NavController) {

  }
 . . . 
 
}
```


