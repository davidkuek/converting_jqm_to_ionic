
# Extra content 

 

## Data Binding
Angularjs offer a fundamental called data binding which allows you to bind data from **.ts** to **.html**.
In JQM, this often refer to `append` or `$()`, however Ionic makes it more efficent and code saving, example:

**JQM:**
```sh
   <h1 id="fruit-topic"></h1>
   <h2 id="fruit-subtopic"></h2>
   
      <ul id ="fruit-list">
         
      </ul>
      <p>There are many more!</p>
      
      <script>
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

      </script>
```

**Ionic:**

On `home.html`:
```sh
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

In your `home.ts`:
 ```sh
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
ngFor is a method to loop through your data in your `.html`.
For JQM will refer as `for loop`, example from pervious:

**JQM:**
```sh
   <h1 id="fruit-topic"></h1>
   <h2 id="fruit-subtopic"></h2>
   
      <ul id ="fruit-list">
         
      </ul>
      <p>There are many more!</p>
      
      <script>
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

      </script>
```

**Ionic:**
```sh
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

Change it to:
```sh
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
ngIf is a method to display a view or a portion of a view only under specific circumstances.
This is similar to JQM *if else statement*. Pervious example:

**JQM:**
```sh
   <h1 id="fruit-topic"></h1>
   <h2 id="fruit-subtopic"></h2>
   
      <ul id ="fruit-list">
         
      </ul>
      <p id="fruit-paragraph"></p>
      
      <script src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
      <script>
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

      </script>
```
   
**Ionic:**
```sh
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





