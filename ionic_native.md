# Ionic Native
Usage of phone functions, please have cordova installed before proceed. 

## Sqlite database
**JQM:**
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
 
**Ionic:**

Install plugin:
 ```sh
$ ionic cordova plugin add cordova-sqlite-storage
$ npm install --save @ionic-native/sqlite
 ```
 
app.module.ts:
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

home.ts:
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
 
*Note: Sqlite in Ionic is not websql in JQM, therefore is not viewable in debug tools.*

*Note: Sqlite usage cause your app not viewable with `ionic serve`, therefore view your app device instead.*

## Cordova Camera
**JQM:**
```sh
<img src="" id="imageFile">

<script>
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
</script>
```

**Ionic:**
Install the camera plugin:
```sh
$ ionic cordova plugin add cordova-plugin-camera
$ npm install --save @ionic-native/camera
```

app.module.ts:
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

home.html:
```sh
  <ion-content padding>
    <img src="{{imageFile}}">
  </ion-content>
```

home.ts:
```sh
import { Camera, CameraOptions } from '@ionic-native/camera';

@Injectable()
export class DatabaseProvider {

imageFile: any;

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
 this.imageFile = imageUri; 

}, (err) => {
 
 console.log('take photo error ') + err;
});
}

openLibrary(){
  var options = {
    sourceType: this.camera.PictureSourceType.PHOTOLIBRARY,
    destinationType: this.camera.DestinationType.DATA_URL,
    // use data_url instead of file_uri for image display from library
    mediaType: this.camera.MediaType.PICTURE
  };
  this.camera.getPicture(options).then((imageData) =>{
  this.imageFile = 'data:image/jpeg;base64,' + imageData;

  },
  (err) =>{
    console.log('Open photo library error') + err;
  });
}
}
```

[Ionic camera docs](https://ionicframework.com/docs/native/camera/)

## File
**JQM:**

*Creating a new persistent file*
```sh
window.requestFileSystem(LocalFileSystem.PERSISTENT, 0, function (fs) {

    console.log('file system open: ' + fs.name);
    fs.root.getFile("newPersistentFile.txt", { create: true, exclusive: false }, function (fileEntry) {

        console.log("fileEntry is file?" + fileEntry.isFile.toString());
        // fileEntry.name == 'someFile.txt'
        // fileEntry.fullPath == '/someFile.txt'
        writeFile(fileEntry, null);

    }, onErrorCreateFile);

}, onErrorLoadFs);

```

*Creating a new temporary file*
```sh
window.requestFileSystem(window.TEMPORARY, 5 * 1024 * 1024, function (fs) {

    console.log('file system open: ' + fs.name);
    createFile(fs.root, "newTempFile.txt", false);

}, onErrorLoadFs);


function createFile(dirEntry, fileName, isAppend) {
    // Creates a new file or returns the file if it already exists.
    dirEntry.getFile(fileName, {create: true, exclusive: false}, function(fileEntry) {

        writeFile(fileEntry, null, isAppend);

    }, onErrorCreateFile);

}


```