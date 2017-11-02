
 
## Creating a new page

JQM:
```sh
<a href="#second-page" data-icon="plus" class="ui-btn-right"></a>
 ```
 
 Ionic:
 1. Run on this command at your project directory
 ```sh
 $ ionic generate page second
 ```

 2. After page successfully generated, open `app.module.ts` in the app folder at `/src/app`, and add:
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

 3. After import in `app.module.ts`, create a onclick function to the button icon on the header we created just now.
 ```sh
 <button ion-button icon-only (click)="secondPage()">
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
  secondPage(){
  this.navCtrl.push(SecondPage);
  }
}
 ```
 *Note: If there is a header in your home page, the secondPage will automaticaly have the back button, which by pressing that will bring you back to the pervious page.*
 
  - [Ionic nav docs](https://ionicframework.com/docs/components/#navigation)
 
## Data Binding
Angularjs offer a fundamental called data binding which allows you to bind data from **.ts** to **.html**.
In JQM, this often refer to `append` or `$()`, however Ionic makes it more efficent and code saving, example:

JQM:
```sh
   <h1 id="fruit-topic">< -- Adding title --></h1>
   <h2>< -- Adding sub title --></h2>
   
      <ul id ="fruit-list">
         < -- To add the data here we can use append method -->
      </ul>
      <p>There are many more!</p>
      <script>
      $( document ).ready(function() {
         var title = "My favourite Fruit";
         var fruit = ["Durian", "Apple", "Orange", "Watermelon", "Grape"];
         var subtitle = "My top favourite fruit is " + fruit[0];
         $('#fruit-topic h1').append(title);
         $('#fruit-topic h2').append(subtitle);
         $('#fruit-topic ul').append("<li>" + fruit[0] + "</li>" + 
                                 "<li>" + fruit[1] + "</li>" +
                                 "<li>" + fruit[2] + "</li>" +
                                 "<li>" + fruit[3] + "</li>" +
                                 "<li>" + fruit[4] + "</li>");
      });

      </script>
```

Ionic:
On `home.html`,insert:
```sh
<ion-content>
   <h1>My Favourite Fruit</h1>
   <h2>My top favourite is durian!</h2>
   
      <ul>
      <li>Durian</li>
      <li>Apple</li>
      <li>Orange</li>
      <li>Watermelon</li>
      <li>Grape</li>
      </ul>
      <p>There are many more!</p>
   
</ion-content>
```

In your `home.ts`:
 ```sh
import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';
import { SecondPage } from '../second/second'; 

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {
// add this
title = 'My Favourite Fruit';
fruits = ['Durian', 'Apple', 'Orange', 'Watermelon', 'Grape'];
favFruit = this.fruit[0];

  constructor(public navCtrl: NavController) {

  }
 . . . 
 
}
 ```

Now change your `home.html`:
```sh
<ion-content>
   <h1>{{title}}</h1>
   <h2>My top favourite is {{favFruit}}!</h2>
   
      <ul>
      <li>{{fruit[0]}}</li>
      <li>{{fruit[1]}}</li>
      <li>{{fruit[2]}}</li>
      <li>{{fruit[3]}}</li>
      <li>{{fruit[4]}}</li>
      </ul>
      <p>There are many more!</p>
   
</ion-content>
```
*The output will be the same as before data binding.* 

### ngFor
ngFor is a method to loop through your data in your `.html`.
For JQM will refer as `for loop`, example from pervious:

JQM:
```sh
   <h1 id="fruit-topic"></h1>
   <h2></h2>
   
      <ul id ="fruit-list">
         < -- To add the data here we can use append method -->
      </ul>
      <p>There are many more!</p>
      <script>
      $( document ).ready(function() {
         var title = "My favourite Fruit";
         var fruit = ["Durian", "Apple", "Orange", "Watermelon", "Grape"];
         var subtitle = "My top favourite fruit is " + fruit[0];
         $('#fruit-topic h1').append(title);
         $('#fruit-topic h2').append(subtitle);
         for(var i = 0; i< fruit.length; i++){
            $('#fruit-topic ul').append("<li>" + fruit[i] + "</li>");
         }
      });

      </script>
```

Ionic:
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

JQM:
```sh
   <h1 id="fruit-topic"></h1>
   <h2></h2>
   
      <ul id ="fruit-list">
         < -- To add the data here we can use append method -->
      </ul>
      <p></p>
      <script>
      $( document ).ready(function() {
         var title = "My favourite Fruit";
         var fruit = ["Durian", "Apple", "Orange", "Watermelon", "Grape"];
         var subtitle = "My top favourite fruit is " + fruit[0];
         $('#fruit-topic h1').append(title);
         $('#fruit-topic h2').append(subtitle);
         
         for(var i = 0; i< fruit.length; i++){
            $('#fruit-topic ul').append("<li>" + fruit[i] + "</li>");
         }
         
         if(fruit.length>3){
         $('#fruit-topic p').append("There are many more!");  
         }
         
      });
```
   
Ionic:
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
*This tells the view to display the paragraph if there more than 3 items in the fruits array data. *

### ngModel
ngModel is method to send data from the `.ts` file to `.html`.

 - [Angular data binding docs](https://angular.io/guide/displaying-data)
 

 
 ## Sqlite database
 JQM:
 ```sh
var dbName = 'Testdb';
var dbVersion = '1.0';
var dbDisplayName = 'Test DB';
var dbSize = 2*1024*1024;
var item_list = []; 

 function createDatabase(){
    var db = openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
    db.transaction(function(tx) {
         var query = 'CREATE TABLE IF NOT EXISTS ITEM_LIST ' +  
                     '([id] INTEGER PRIMARY KEY AUTOINCREMENT, [name] TEXT,[desc] TEXT);';
            tx.executeSql(query)
         },
         function(err){
            console.log('create database error ' + err)
            });
 }
 
 function displayItemList(){
var query = "SELECT * FROM ITEM_LIST;";
    db = openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
    db.transaction(function (tx){
        tx.executeSql(query,[],
            function(tx,results){
                if (results.rows.length > 0) {
                    for(var i=0; i < results.rows.length; i++){
                        item_list[i] = [];
                        item_list[i][0] = results.rows.item(i).id;
                        item_list[i][1] = results.rows.item(i).name;
                        item_list[i][2] = results.rows.item(i).desc;
                            
                    }
            }               
            },
            function(err){
                console.log('display item list error ' + err);
            });
    },function(err){
        console.log('Open database error' + err);
    });


}
 ```
 
 Ionic:
 1.  Install plugin
 ```sh
$ ionic cordova plugin add cordova-sqlite-storage
$ npm install --save @ionic-native/sqlite
 ```
 
 2. Import into app.module.ts
 ```sh
 ...

import { SQLite } from '@ionic-native/sqlite';

...

@NgModule({
  ...

  providers: [
    ...
    SQLite
    ...
  ]
  ...
})
export class AppModule { }
```

3. Import to home.ts
```sh
import { SQLite, SQLiteObject } from '@ionic-native/sqlite';

@Injectable()
export class DatabaseProvider {

item_list = [];


constructor(private sqlite: SQLite) { }

...

createDatabase(){
this.sqlite.create({
  name: 'Test.db',
  location: 'default'
})
  .then((db: SQLiteObject) => {
   
   let query = 'CREATE TABLE IF NOT EXISTS ITEM_LIST ' +  
               '([id] INTEGER PRIMARY KEY AUTOINCREMENT, [name] TEXT,[desc] TEXT);';
   
    db.executeSql(query, [])
      .then(() => console.log('Executed SQL'))
      .catch(e => console.log('execute sql error ') + e);

  })
  .catch(e => console.log('sqlite create ' + e));
  }


  displayDatabase(){
  // you have to use create method again to check whether the database is created
      this.sqlite.create({
        name: 'Test.db',
        location: 'default'
      })
      .then((db: SQLiteObject) => {

          let output = [];
          let query = "SELECT * FROM ITEM_LIST;";
          db.executeSql(query,[])
          .then((results) => {

             if (results.rows.length > 0) {
                for (var i = 0; i < results.rows.length; i++) {
          
                        item_list[i] = [];
                        item_list[i][0] = results.rows.item(i).id;
                        item_list[i][1] = results.rows.item(i).name;
                        item_list[i][2] = results.rows.item(i).desc;
                 }
              }
    
           },(error) =>{
             console.log('Execute sql ' + error);
   })
   
       })
   .catch(e => console.error('Open database error ' + e));

  }
  
  }
```
 
## Cordova Camera
JQM:
```sh
function setOptions(srcType) {
    var options = {
        // Some common settings are 20, 50, and 100
        quality: 50,
        destinationType: Camera.DestinationType.FILE_URI,
        sourceType: srcType,
        encodingType: Camera.EncodingType.JPEG,
        mediaType: Camera.MediaType.PICTURE,
        allowEdit: false,
        correctOrientation: true
    }
    return options;
}

function openCamera(selection) {

    var srcType = Camera.PictureSourceType.CAMERA;
    var options = setOptions(srcType);

    navigator.camera.getPicture(function cameraSuccess(imageUri) {

        displayImage(imageUri);
        
    }, function cameraError(error) {
        console.log('camera '+error);

    }, options);
}


function openLibrary(selection) {

    var srcType = Camera.PictureSourceType.SAVEDPHOTOALBUM;
    var options = setOptions(srcType);

    navigator.camera.getPicture(function cameraSuccess(imageUri) {

        displayImage(imageUri);

    }, function cameraError(error) {
        console.log('open image ' + error);

    }, options);
}

function displayImage(imageUri) {

    var elem = document.getElementById('imageFile');
    elem.src = imageUri;
}
```

Ionic:
1. Install the camera plugin.
```sh
$ ionic cordova plugin add cordova-plugin-camera
$ npm install --save @ionic-native/camera
```

2. Add this to app.module.ts
```sh
...

import { Camera } from '@ionic-native/camera';

...

@NgModule({
  ...

  providers: [
    ...
    Camera
    ...
  ]
  ...
})
export class AppModule { }

```

3. In home.ts:
```sh
import { Camera, CameraOptions } from '@ionic-native/camera';

@Injectable()
export class DatabaseProvider {

image: any;

constructor(private camera: Camera) { }

...
 options: CameraOptions = {
  quality: 100,
  destinationType: this.camera.DestinationType.FILE_URI,
  encodingType: this.camera.EncodingType.JPEG,
  mediaType: this.camera.MediaType.PICTURE,
  sourceType: this.camera.PictureSourceType.CAMERA,
  correctOrientation: true
}


openCamera(){
this.camera.getPicture(this.options).then((imageUri) => {
 this.image = imageUri; 

}, (err) => {
 
 console.log('take photo error ') + err;
});
}

openLibrary(){
  var options = {
    sourceType: this.camera.PictureSourceType.PHOTOLIBRARY,
    destinationType: this.camera.DestinationType.DATA_URL,
    mediaType: this.camera.MediaType.PICTURE
  };
  this.camera.getPicture(options).then((imageData) =>{
  this.image= 'data:image/jpeg;base64,' + imageData;

  },
  (err) =>{
    console.log('Open photo library error') + err;
  });
}
}
```
