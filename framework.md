# The UI component

- [Header](#header)
- [Footer](#footer)
- [Buttons](#buttons)
- [Lists](#lists)
- [Inputs](#inputs)
- [Checkbox](#checkbox)
- [Radio](#radio)
- [Searchbar](#searchbar)
- [Menu](#menu)
- [Alert](#alert)
- [Datepicker](#datepicker)

## <a name="header"></a>Header
**JQM**:
```sh
<div data-role="header">
  <h1>Copy this</h1>
    </div>
```

**Ionic:**
```sh
<ion-header>
  <ion-navbar>
    <ion-title>
      To here
    </ion-title> 
  </ion-navbar>
</ion-header>

<!-- Theming-->
<ion-header>
  <ion-navbar color="primary"> 
    <ion-title>
      Page Name
    </ion-title> 
  </ion-navbar>
</ion-header>
```

*Custom color at scss file:*
```sh
$colors: (
  primary:    #488aff, <-- you can modify the color code from here -->
  secondary:  #32db64,
  danger:     #f53d3d,
  light:      #f4f4f4,
  dark:       #222
);
```

[Ionic Header Docs](https://ionicframework.com/docs/api/components/toolbar/Header/)
[Ionic scss Theming Docs](https://ionicframework.com/docs/theming/theming-your-app/)
 
<a href="#top">Back to top</a>

## <a name="footer">Footer
**JQM**:
```sh
<div data-role="footer">
<h1>Footer</h1>
</div>
```
**Ionic:**
```sh
<ion-content></ion-content>

<ion-footer>
  <ion-toolbar>
    <ion-title>Footer</ion-title>
  </ion-toolbar>
</ion-footer>
```

[Ionic Footer Docs](https://ionicframework.com/docs/api/components/toolbar/Footer/)

<a href="#top">Back to top</a>

## <a name="buttons">Buttons
**JQM**: 
```sh
<a href="#" class="ui-btn">Button</a>
<button class="ui-btn">Button</button>

<!-- Onclick-->
<button class="ui-btn" onclick="someFunction(event)">Button</button>

<!-- Theming-->
<button class="ui-btn ui-btn-a">Button</button>

<!-- Icons -->
<a href="#" class="ui-btn ui-icon-star ui-btn-icon-left">Left Icon</a>
<button class="ui-btn ui-icon-star ui-btn-icon-left">Left Icon</button>

<a href="#" class="ui-btn ui-icon-star ui-btn-icon-right">Right Icon</a>
<button class="ui-btn ui-icon-star ui-btn-icon-right">Right Icon</button>

<!-- Icons only -->
<a href="#" class="ui-btn ui-icon-star ui-btn-icon-notext"></a>
```

**Ionic:**
```sh
<button ion-button>Button</button>

<!-- Onclick-->
<button ion-button (click)="someFunction($event)">Button</button>

<!-- Theming-->
<button ion-button color="secondary">Secondary</button>

<!-- Icons -->
<button ion-button icon-start>
  <ion-icon name="star"></ion-icon>
  Left Icon
</button>

<button ion-button icon-end>
  Right Icon
  <ion-icon name="star"></ion-icon>
</button>

<!-- Icons only -->
<button ion-button icon-only>
  <ion-icon name="star"></ion-icon>
</button>
```

[Ionic button framework docs](https://ionicframework.com/docs/components/#buttons)
[Ionic button api docs](https://ionicframework.com/docs/api/components/button/Button/)

<a href="#top">Back to top</a>

## <a name="lists">Lists
**JQM**
```sh
<!-- Basic linked list -->
<ul data-role="listview">
    <li><a href="#">Acura</a></li>
    <li><a href="#">Audi</a></li>
    <li><a href="#">BMW</a></li>
    <li><a href="#">Cadillac</a></li>
    <li><a href="#">Ferrari</a></li>
</ul>

<!-- Inset linked list -->  
<ul data-role="listview" data-inset="true">
    <li><a href="#">Acura</a></li>
    <li><a href="#">Audi</a></li>
    <li><a href="#">BMW</a></li>
    <li><a href="#">Cadillac</a></li>
    <li><a href="#">Ferrari</a></li>
</ul>

<!-- List dividers -->  
<ul data-role="listview" data-inset="true" data-divider-theme="a">
    <li data-role="list-divider">Mail</li>
    <li><a href="#">Inbox</a></li>
    <li><a href="#">Outbox</a></li>
    <li data-role="list-divider">Contacts</li>
    <li><a href="#">Friends</a></li>
    <li><a href="#">Work</a></li>
</ul>

<!-- Thumbnail-->  
<ul data-role="listview" data-inset="true">
    <li><a href="#">
        <img src="../_assets/img/album-bb.jpg">
    <h2>Broken Bells</h2>
    <p>Broken Bells</p></a>
    </li>
    <li><a href="#">
        <img src="../_assets/img/album-hc.jpg">
    <h2>Warning</h2>
    <p>Hot Chip</p></a>
    </li>
    <li><a href="#">
        <img src="../_assets/img/album-p.jpg">
    <h2>Wolfgang Amadeus Phoenix</h2>
    <p>Phoenix</p></a>
    </li>
</ul>

```

**Ionic:**
```sh
<!-- Basic linked list -->
<ion-list>
  <button ion-item>Acura</button>  
  <button ion-item>Audi</button>  
  <button ion-item>BMW</button>  
  <button ion-item>Cadillac</button>  
  <button ion-item>Ferrari</button>  
</ion-list>

<!-- Inset linked list -->
<ion-list inset>
  <button ion-item>Acura</button>  
  <button ion-item>Audi</button>  
  <button ion-item>BMW</button>  
  <button ion-item>Cadillac</button>  
  <button ion-item>Ferrari</button> 
</ion-list>

<!-- List dividers -->  
  <ion-item-group>
    <ion-item-divider color="light">Mail</ion-item-divider>
  <button ion-item>Inbox</button>  
  <button ion-item>Outbox</button>
  </ion-item-group>
  <ion-item-group>
    <ion-item-divider color="light">Contacts</ion-item-divider>
  <button ion-item>Friends</button>  
  <button ion-item>Work</button>
  </ion-item-group>

<!-- Thumbnail-->  
<ion-list>
  <button ion-item>
    <ion-thumbnail item-start>
      <img src="../_assets/img/album-bb.jpg">
    </ion-thumbnail>
    <h2>Broken Bells</h2>
    <p>Broken Bells</p>
  </button>
  <button ion-item>
    <ion-thumbnail item-start>
      <img src="../_assets/img/album-hc.jpg">
    </ion-thumbnail>
    <h2>Warning</h2>
    <p>Hot Chip</p>
  </button>
  <button ion-item>
    <ion-thumbnail item-start>
      <img src="../_assets/img/album-p.jpg">
    </ion-thumbnail>
    <h2>Wolfgang Amadeus Phoenix</h2>
    <p>Phoenix</p>
  </button>
</ion-list>
```

[Ionic list](https://ionicframework.com/docs/components/#lists)
 
<a href="#top">Back to top</a>

## <a name="inputs">Inputs
**JQM**:
```sh
<!-- Text-->  
<label for="text-basic">Username:</label>
<input name="text-basic" id="text-basic" value="" type="text">

<!-- Password--> 
<label for="password">Password:</label>
<input name="password" id="password" value="" autocomplete="off" type="password">

<!-- Text Area--> 
<label for="textarea-1">Textarea:</label>
<textarea name="textarea-1" id="textarea-1"></textarea>

<!-- Clear Input-->
<label for="text-basic">Username:</label>
<input name="text-basic" id="text-basic" value="" type="text" data-clear-btn="true"

```

**Ionic:**
```sh
<ion-list>

<!-- Text--> 
  <ion-item>
    <ion-label>Username</ion-label>
    <ion-input type="text" value=""></ion-input>
  </ion-item>

<!-- Password--> 
  <ion-item>
    <ion-label>Password</ion-label>
    <ion-input type="password"></ion-input>
  </ion-item>

<!-- Text Area--> 
  <ion-item>
    <ion-label>Textarea</ion-label>
    <ion-input type="textarea" value=""></ion-input>
  </ion-item>

<!-- Clear Input-->
   <ion-item>
    <ion-label>Clear Input</ion-label>
    <ion-input type="text" value="" clearInput></ion-input>
  </ion-item>
</ion-list>
```

[Ionic input framework doc](https://ionicframework.com/docs/components/#inputs)
[Ionic input api doc](https://ionicframework.com/docs/api/components/input/Input/)
 
<a href="#top">Back to top</a>

## <a name="checkbox">CheckBox
**JQM:**
```sh
<!-- Basic-->
    <label>
        <input name="checkbox-0 " type="checkbox">Check me
    </label>


<!-- Disabled-->
    <label>
        <input name="checkbox-0 " type="checkbox" disabled="">Check me
    </label>
```

**Ionic:**
```sh
<ion-list>
<!-- Basic-->
  <ion-item>
    <ion-label>Check me</ion-label>
    <ion-checkbox></ion-checkbox>
  </ion-item>

<!-- Disabled-->
  <ion-item>
    <ion-label>Check me</ion-label>
    <ion-checkbox disabled="true"></ion-checkbox>
  </ion-item>
</ion-list>
```

[Ionic checkbox framework docs](https://ionicframework.com/docs/components/#checkbox)
[Ionic checkbox api docs](https://ionicframework.com/docs/api/components/checkbox/Checkbox/)
 
<a href="#top">Back to top</a>

## <a name="radio">Radio
**JQM**:
```sh
<fieldset data-role="controlgroup">
    <legend>Radio buttons, vertical controlgroup:</legend>
        <input name="radio-choice-1" id="radio-choice-1" value="choice-1" checked="checked" type="radio">
        <label for="radio-choice-1">Cat</label>
        <input name="radio-choice-1" id="radio-choice-2" value="choice-2" type="radio">
        <label for="radio-choice-2">Dog</label>
        <input name="radio-choice-1" id="radio-choice-3" value="choice-3" type="radio">
        <label for="radio-choice-3">Hamster</label>
        <input name="radio-choice-1" id="radio-choice-4" value="choice-4" type="radio">
        <label for="radio-choice-4">Lizard</label>
</fieldset>
```

**Ionic:**
```sh
<ion-list radio-group>
  <ion-list-header>
    Radio buttons, vertical controlgroup:
  </ion-list-header>

  <ion-item>
    <ion-label>Cat</ion-label>
    <ion-radio checked="true" value="choice-1"></ion-radio>
  </ion-item>

  <ion-item>
    <ion-label>Dog</ion-label>
    <ion-radio value="choice-2"></ion-radio>
  </ion-item>

  <ion-item>
    <ion-label>Hamster</ion-label>
    <ion-radio value="choice-3"></ion-radio>
  </ion-item>

  <ion-item>
    <ion-label>Lizard</ion-label>
    <ion-radio value="choice-4"></ion-radio>
  </ion-item>
</ion-list>

```

[Ionic radio docs](https://ionicframework.com/docs/components/#radio)
 
<a href="#top">Back to top</a>

## <a name="searchbar">Searchbar

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
 
<a href="#top">Back to top</a>

## <a name="menu">Menu
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
 
<a href="#top">Back to top</a>

## <a name="alert">Alert
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

<a href="#top">Back to top</a>

## <a name="datepicker">Datepicker
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

<a href="#top">Back to top</a>

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



