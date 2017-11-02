
# Api 
## Basic alert
**JQM:**
```sh
<button onclick="popAlert()">Alert</button>
<script>
function popAlert(){
  alert('New alert!');
}
</script>
```

**Ionic:**

home.html
```sh
<button ion-button (click)="popAlert()">Button</button>
```

home.ts
```sh
import { AlertController } from 'ionic-angular';

export class MyPage {
  constructor(public alertCtrl: AlertController) {
  }

  popAlert() {
    let alert = this.alertCtrl.create({
      title: 'Alert',
      subTitle: 'New Alert!',
      buttons: ['OK']
    });
    alert.present();
  }
}
```

[Ionic alert docs](https://ionicframework.com/docs/components/#alert)


## Datepicker
**JQM:**
```sh
<input data-role="date" data-inline="true" type="text">
```

**Ionic:**
```sh
<ion-item>
  <ion-label>Date</ion-label>
  <ion-datetime displayFormat="MM/DD/YYYY" [(ngModel)]="myDate"></ion-datetime>
</ion-item>
```

[Ionic datepicker docs](https://ionicframework.com/docs/api/components/datetime/DateTime/)


## Creating a new page

**JQM:**
```sh
<a href="#second-page" class="ui-btn">Next page</a>

<!-- Second page -->
<div data-role="page" id="second-page" >
</div>
 ```
 or
 ```sh
 <button ion-button onclick="nextPage()">Next Page</button>

 <!-- Second page -->
<div data-role="page" id="second-page" >

 <script>
 function nextPage(){
  $.mobile.navigate( "#second-page" );
 }
 </script>
 ```
 
**Ionic:**

 1. Run on terminal inside your directory:
 ```sh
 $ ionic generate page second
 ```

[More ionic cli docs](https://ionicframework.com/docs/cli/)

 2. Open `app.module.ts` at /src/app.
```sh
import { BrowserModule } from '@angular/platform-browser';
import { ErrorHandler, NgModule } from '@angular/core';
import { IonicApp, IonicErrorHandler, IonicModule } from 'ionic-angular';
import { SplashScreen } from '@ionic-native/splash-screen';
import { StatusBar } from '@ionic-native/status-bar';

import { MyApp } from './app.component';
import { HomePage } from '../pages/home/home';
import { SecondPage } from '../pages/second/second' // import in here

@NgModule({
  declarations: [
    MyApp,
    HomePage,
    SecondPage  // declare at here
  ],
  imports: [
    BrowserModule,
    IonicModule.forRoot(MyApp)
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp,
    HomePage,
    SecondPage   // and here
  ],
  providers: [
    StatusBar,
    SplashScreen,
    {provide: ErrorHandler, useClass: IonicErrorHandler}
  ]
})
export class AppModule {}
 ```

 3. Create onclick function on a button.
 ```sh
 <button ion-button icon-only (click)="nextPage()">Next Page</button>
 ```
 4. On `home.ts`:
```sh
import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';
import { SecondPage } from '../second/second'; //import again but different path

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  constructor(public navCtrl: NavController) {

  }
  
  // assign navCtrl to the onclick function
  nextPage(){
  this.navCtrl.push(SecondPage);
  }
}
 ```
 *Note: If there is a header in your home page, the secondPage will automaticaly have the back button, which by pressing that will bring you back to the pervious page.*
 
  - [Ionic nav docs](https://ionicframework.com/docs/components/#navigation)
 

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

## Searchbar

**JQM:**
```sh
<ul data-role="listview" data-filter="true" data-filter-placeholder="Search fruits..." data-inset="true">
    <li><a href="#">Apple</a></li>
    <li><a href="#">Banana</a></li>
    <li><a href="#">Cherry</a></li>
    <li><a href="#">Cranberry</a></li>
    <li><a href="#">Grape</a></li>
    <li><a href="#">Orange</a></li>
</ul>
```

**Ionic:**
home.html
```sh
<ion-searchbar (ionInput)="getItems($event)"></ion-searchbar>
<ion-list>
  <ion-item *ngFor="let fruit of fruits">
    {{ fruit }}
  </ion-item>
</ion-list>
```

home.ts
```sh
@Component({
  templateUrl: 'search/template.html',
})
class SearchPage {

fruits = [];

  constructor() {
    this.initializeItems();
  }

  initializeItems() {
    this.fruits = [
      'Apple',
      'Banana',
      'Cherry',
      'Cranberry',
      'Grape',
      'Orange'
    ];
  }

  getItems(ev: any) {
    // Reset items back to all of the items
    this.initializeItems();

    // set val to the value of the searchbar
    let val = ev.target.value;

    // if the value is an empty string don't filter the items
    if (val && val.trim() != '') {
      this.fruits = this.fruits.filter((item) => {
        return (item.toLowerCase().indexOf(val.toLowerCase()) > -1);
      })
    }
  }
}
```
 
[Ionic searchbar component](https://ionicframework.com/docs/components/#searchbar)
[Ionic searchbar api](https://ionicframework.com/docs/api/components/searchbar/Searchbar/)

## Menu
**JQM:**
```sh
<div data-role="page">
  <div data-role="header">
    <a href="#mypanel" class="ui-btn ui-shadow ui-corner-all ui-btn-inline ui-btn-icon-left ui-icon-bars"></a>
  </div>
    <div data-role="panel" id="mypanel" data-display="overlay">
      <div data-role="header">
          <h1>Menu</h1>
      </div>
        <p>Menu Content</p>
    </div>
</div>
```

**Ionic:**

home.html:
```sh
<ion-header>
  <ion-navbar>
     <button ion-button icon-left menuToggle>
      <ion-icon name='menu'></ion-icon>
    </button>
    <ion-title>
      
    </ion-title>
  </ion-navbar>
</ion-header>

<ion-content padding>

</ion-content>

```

app.html (/src/app):
```sh
<ion-menu type="overlay" [content]="mycontent">
<ion-header>
  <ion-navbar>
    <ion-title>
      Menu
    </ion-title>
  </ion-navbar>
</ion-header>

  <ion-content padding>
    <ion-list>
      <p>Menu content</p>
    </ion-list>
  </ion-content>
</ion-menu>

<ion-nav #mycontent [root]="rootPage"></ion-nav>
```

[Ionic menu api docs](https://ionicframework.com/docs/api/components/menu/Menu/)




