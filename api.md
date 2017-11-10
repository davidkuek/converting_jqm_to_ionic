#Api

- [Nav](#button)

## <a name="mobileinit">MobileInit
**JQM:**
```sh
$( document ).on( "mobileinit", function() {
	// init something here
});
```

**Ionic:**

*app.component.ts:*
```sh
import { Component } from '@angular/core';
import { Platform } from 'ionic-angular';
import { StatusBar } from '@ionic-native/status-bar';
import { SplashScreen } from '@ionic-native/splash-screen';

import { HomePage } from '../pages/home/home';
@Component({
  templateUrl: 'app.html'
})
export class MyApp {
  rootPage:any = HomePage;

  constructor(platform: Platform, statusBar: StatusBar, splashScreen: SplashScreen) {
    platform.ready().then(() => {
      
      // init here

      statusBar.styleDefault();
      splashScreen.hide();
    });
  }
}
```


## <a name="pageinit">PageInit
**JQM:**
```sh
$( document ).on( "pageinit", "#aboutPage", function( event ) {
  // init something for the page #aboutPage
});
```


**Ionic:**
```sh
import { Platform } from 'ionic-angular'; //import

@Component({
  selector: 'page-about',
  templateUrl: 'about.html'
})
export class AboutPage {

	//insert into constructor
  constructor(private platform: Platform) {

  	//apply
  this.platform.ready().then(() => {
  	//init for this page
	});
  }
}

```



## <a name="navigate">Navigate
**JQM:**
```sh
<a href="#second-page" class="ui-btn">Next page</a>

<!-- Second page -->
<div data-role="page" id="second-page" >
</div>
 ```
 or
 ```sh
 <button onclick="nextPage()">Next page</button>

 <!-- Second page -->
<div data-role="page" id="second-page" >

 <script>
 function nextPage(){
  $.mobile.navigate( "#second-page" );
 }
 </script>
 ```
 
**Ionic:**

 1. Create a page with terminal:
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

 3. home.html:
 ```sh
 <button ion-button icon-only (click)="nextPage()">Next Page</button>
 ```
 4. home.ts:
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





