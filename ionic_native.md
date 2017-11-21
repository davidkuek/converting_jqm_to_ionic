# Ionic Native
Usage of phone functions, please have cordova installed before proceed. 

- [SQLite database](#sqlite)
- [Camera](#camera)
- [File](#file)
- [Geolocation](#geolocation)

## <a name="sqlite">Sqlite database
**JQM:**
 ```js
var dbName = 'Testdb';
var dbVersion = '1.0';
var dbDisplayName = 'Test DB';
var dbSize = 2*1024*1024;
var item_list = []; 

// creating tables
function createDatabase(){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = 'CREATE TABLE IF NOT EXISTS ITEM_LIST ' +  
            '([id] INTEGER PRIMARY KEY AUTOINCREMENT, [name] TEXT,[desc] TEXT);';

    db.transaction(function(tx){
        tx.executeSql(query, [],function(tx,result){
            console.log('executed Sql:' + result);
        },sqlError);
    },dbError);
}
 
// updating item in tables
function updateItem(id,name,desc){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = 'UPDATE ITEM_LIST SET NAME = ?, DESC = ? WHERE ID = ?;';

    db.transaction(function(tx){
        tx.executeSql(query,[name,desc,id],function(tx,result){
            console.log('executed sql:' + result);
        },sqlError);
    },dbError);  
}

// delete item in tables
function deleteItem(id){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = 'DELETE FROM ITEM_LIST WHERE ID =?;';

    db.transaction(function(tx){
        tx.executeSql(query,[id],function(tx,result){
            console.log('executed sql ' + result);
        },sqlError);
    },dbError);  

}

// adding  item in tables
function addItem(name,desc){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = 'INSERT INTO ITEM_LIST(name,desc) VALUES (?,?);';

    db.transaction(function(tx){
        tx.executeSql(query,[name,desc],function(tx,result){
            console.log('executed sql ' + result);
        },sqlError);
    },dbError);  
}

// show table item
 function displayItemList(){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = "SELECT * FROM ITEM_LIST;";
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

                    console.log(item_list);
                } 
                              
            },sqlError);

    },dbError);
}

// error handler
var sqlError = function(err){
    console.log('sql executed error:' + err);
}

var dbError = function(err){
    console.log('db transaction error:' + err);
}
 ```
 
**Ionic:**


*Note: Sqlite in Ionic is not websql in JQM, therefore is not viewable in debug tools.*

*Note: Sqlite usage may cause your app not viewable with `ionic serve`, therefore view your app device instead.*

Steps before using:

1. *Install plugin:*
```sh
$ ionic cordova plugin add cordova-sqlite-storage
$ npm install --save @ionic-native/sqlite
```
 
2. *app.module.ts:*
```ts
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

3. *home.ts:*
```ts
import { SQLite, SQLiteObject } from '@ionic-native/sqlite'; //import this

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  item_list = [];

  constructor(private sqlite: SQLite) { // inject this

  }

// creating tables
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


// updating item in tables
updateItem(id,name,desc){
this.sqlite.create({
  name: 'Test.db',
  location: 'default'
})
  .then((db:SQLiteObject)=>{

    let query = 'UPDATE ITEM_LIST SET NAME = ?, DESC = ? WHERE ID = ?;';

    db.executeSql(query,[name,desc,id])
    .then(()=>console.log('Executed SQL'))
    .catch(e=>console.log('executed SQL error ' + e));
  })
  .catch(e=>console.log('sqlite update error' + e));
}

// deleting item in tables
deleteItem(id){
this.sqlite.create({
  name: 'Test.db',
  location: 'default'
})
  .then((db:SQLiteObject)=>{

    let query = 'DELETE FROM ITEM_LIST WHERE ID =?;';

    db.executeSql(query,[id])
    .then(()=>console.log('Executed SQL'))
    .catch(e=>console.log('executed SQL error ' + e));
  })
  .catch(e=>console.log('sqlite update error' + e));
}


// adding item in tables
addItem(name,desc){
this.sqlite.create({
  name: 'Test.db',
  location: 'default'
})
  .then((db:SQLiteObject)=>{

    let query = 'INSERT INTO ITEM_LIST(name,desc) VALUES (?,?);';

    db.executeSql(query,[name,desc])
    .then(()=>console.log('Executed SQL'))
    .catch(e=>console.log('executed SQL error ' + e));
  })
  .catch(e=>console.log('sqlite update error' + e));
}

// show data from tables
 displayItem(){
      this.sqlite.create({
        name: 'Test.db',
        location: 'default'
      })
      .then((db: SQLiteObject) => {

          let query = "SELECT * FROM ITEM_LIST;";
          db.executeSql(query,[])
          .then((results) => {

             if (results.rows.length > 0) {
                for (var i = 0; i < results.rows.length; i++) {
          
                        this.item_list[i] = [];
                        this.item_list[i][0] = results.rows.item(i).id;
                        this.item_list[i][1] = results.rows.item(i).name;
                        this.item_list[i][2] = results.rows.item(i).desc;
                 }
              }
    
           })
    .catch(e=>console.log('execute SQL error' + e));
   
       })
   .catch(e => console.error('Open database error ' + e));

  }
}
```

[Ionic SQLite Docs](https://ionicframework.com/docs/native/sqlite/)

<a href="#top">Back to top</a>

  

## <a name="camera">Camera
**JQM:**
```html
<img src="" id="imageFile">

<script>
// camera options
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

// take photo with camera
function openCamera(selection) {

    var srcType = Camera.PictureSourceType.CAMERA;
    var options = setOptions(srcType);

    navigator.camera.getPicture(function cameraSuccess(imageUri) {

        displayImage(imageUri);
        
    }, function cameraError(error) {
        console.log('camera '+error);

    }, options);
}

// choose photo from album
function openLibrary(selection) {

    var srcType = Camera.PictureSourceType.SAVEDPHOTOALBUM;
    var options = setOptions(srcType);

    navigator.camera.getPicture(function cameraSuccess(imageUri) {

        displayImage(imageUri);

    }, function cameraError(error) {
        console.log('open image ' + error);

    }, options);
}

// displaying image on view
function displayImage(imageUri) {

    var elem = document.getElementById('imageFile');
    elem.src = imageUri;
}
</script>
```

**Ionic:**

Steps before using:

1. *Install the camera plugin:*
```sh
$ ionic cordova plugin add cordova-plugin-camera
$ npm install --save @ionic-native/camera
```

2. *app.module.ts:*
```ts
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

3. *home.html:*
```html
  <ion-content padding>
    <img src="{{imageFile}}">
  </ion-content>
```

4. *home.ts:*
```ts
import { Camera, CameraOptions } from '@ionic-native/camera';

@Injectable()
export class DatabaseProvider {

imageFile: any;

constructor(private camera: Camera) { }

...

// setting options
 options: CameraOptions = {
  quality: 100,
  destinationType: this.camera.DestinationType.FILE_URI,
  encodingType: this.camera.EncodingType.JPEG,
  mediaType: this.camera.MediaType.PICTURE,
  sourceType: this.camera.PictureSourceType.CAMERA,
  correctOrientation: true
}

// Android take photo
openCamera(){
this.camera.getPicture(this.options).then((imageUri) => {
 this.imageFile = imageUri; 

}, (err) => {
 
 console.log('take photo error ') + err;
});
}

//ios take photo
openCamera(){
this.camera.getPicture(this.options).then((imageUri) => {
 this.imageFile = imageUri.replace(/^file:\/\//, '');

}, (err) => {
 
 console.log('take photo error ') + err;
});
}

// choose photo from library
openLibrary(){
  var options = {
    sourceType: this.camera.PictureSourceType.PHOTOLIBRARY,
    destinationType: this.camera.DestinationType.DATA_URL, // use data_url instead of file_uri for image display from library
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

<a href="#top">Back to top</a>

## <a name="file">File
[Different platform file location guide](https://ionicframework.com/docs/native/file/#instance-members)

**JQM:**

```js
// creating file
function createFile(){
    var path = cordova.file.dataDirectory;

window.resolveLocalFileSystemURL(path,function(fs) {

    fs.getFile("someFile.txt", { create: true, exclusive: false }, function (fileEntry) {
        
        console.log(fileEntry.fullPath);
        
    }, onErrorGetFile);

}, onErrorLoadFs);

}

// write content in file
function writeFile(fileEntry, dataObj, isAppend) {
    
    var path = cordova.file.dataDirectory;
    
    window.resolveLocalFileSystemURL(path, function(fs){
    
          fs.getFile('someFile.txt',{create:false}, function(fileEntry) {
    
             fileEntry.createWriter(function(fileWriter) {
                fileWriter.onwriteend = function(e) {
                   console.log('Write completed.');
                };
    
                fileWriter.onerror = function(e) {
                   console.log('Write failed: ' + e.toString());
                };
    
                var blob = new Blob(['Lorem Ipsum'], {type: 'text/plain'});
                fileWriter.write(blob);
    
             }, onErrorWriteFile);
    
          }, onErrorGetFile);
    
       }, onErrorLoadFs);
    
    }
    
// display content from file
function readFile() {

    var path = cordova.file.dataDirectory;

    window.resolveLocalFileSystemURL(path, function(fs){
      fs.getFile('someFile.txt', {}, function(fileEntry) {

         fileEntry.file(function(file) {
            var reader = new FileReader();

            reader.onloadend = function(e) {
               console.log(this.result);
            };

            reader.readAsText(file);

         }, onErrorReadFile);

      }, onErrorGetFile);

   }, onErrorLoadFs)

}

// delete file
function removeFile() {

    var path = cordova.file.dataDirectory;
    
    window.resolveLocalFileSystemURL(path, function(fs){
    
          fs.getFile('someFile.txt', {create: false}, function(fileEntry) {
    
             fileEntry.remove(function() {
                console.log('File removed.');
    
             }, onErrorDeleteFile);
    
          }, onErrorGetFile);
    
       }, onErrorLoadFs);
    }   
    
// create folder
function createDirectory(rootDirEntry) {

    var path = cordova.file.dataDirectory;

window.resolveLocalFileSystemURL(path, function(rootDirEntry) {        
rootDirEntry.getDirectory('NewDirInRoot', { create: true }, function (dirEntry) {
    dirEntry.getDirectory('subDir', { create: true }, function (subDirEntry) {

        console.log('directory created' + dirEntry.fullPath);

    });
});
});
}

var onErrorGetFile = function(err){
    console.log('get file error:' + err.code);
}

var onErrorLoadFs = function(err){
    console.log('load fs error:' + err.code);
}

var onErrorWriteFile = function(err){
    console.log('write file error:' + err.code);
}

var onErrorReadFile = function(err){
    console.log('read file error:' + err.code);
}

var onErrorDeleteFile = function(err){
    console.log('delete file error:' + err.code);
}



```

**Ionic**

*Install the plugin:*
```sh
$ ionic cordova plugin add cordova-plugin-file
$ npm install --save @ionic-native/file
```

*app.module.ts:*
```ts
import { File } from '@ionic-native/file';

  providers: [
    File   
  ]
})
export class AppModule {}
```

*home.ts:*
```ts
import { File } from '@ionic-native/file';


@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  constructor(public navCtrl: NavController,private file: File) {

  }

// create file
createFile(){

  let path = this.file.dataDirectory;
  let fileName = 'someFile.txt';
  let isAppend = true;
  // true replace file with same name, false returns error

  this.file.createFile(path, fileName,isAppend)
  .then(file => console.log('created' + file.fullPath))
  .catch(err => console.log(err))
  }

// write content into file
writeFile(){

  let path = this.file.dataDirectory;
  let fileName = 'someFile.txt';
  let textContent = 'Lorem Ipsum';
  let text = new Blob([textContent],{type:'text/plain'});

  this.file.writeFile(path, fileName, text, {replace:true})
  .then(() => console.log('write success: ' + textContent))
  .catch(err => console.log(err))
}

// display content from file
readFile(){

  let path = this.file.dataDirectory;
  let fileName = 'someFile.txt';


  this.file.readAsText(path,fileName)
  .then((result)=>console.log(result))
  .catch(err=> console.log(err))

}

// delete file
removeFile(){

  let path = this.file.dataDirectory;
  let fileName = 'someFile.txt';

  this.file.removeFile(path,fileName)
  .then((result)=>console.log(result))
  .catch(err => console.log(err))
}

// create folder
createDir(){

  let path = this.file.dataDirectory;
  let dirName = 'ionicFile';
  let replace = true;

  this.file.createDir(path,dirName,replace)
  .then((result)=>console.log(result))
  .catch(err=> console.log(err))

}

}

```

[Ionic file docs](https://ionicframework.com/docs/native/file/)

<a href="#top">Back to top</a>

## <a name="geolocation">Geolocation
**JQM:**
```js
var watchID;

var getPositionSuccess = function(position) {
    console.log('Latitude: '          + position.coords.latitude          + '\n' +
                'Longitude: '         + position.coords.longitude         + '\n' +
                'Altitude: '          + position.coords.altitude          + '\n' +
                'Accuracy: '          + position.coords.accuracy          + '\n' +
                'Altitude Accuracy: ' + position.coords.altitudeAccuracy  + '\n' +
                'Heading: '           + position.coords.heading           + '\n' +
                'Speed: '             + position.coords.speed             + '\n' +
                'Timestamp: '         + position.timestamp                + '\n');

};


var watchPositionSuccess = function(position) {
    var element = document.getElementById('geolocation');
    element.innerHTML = 'Latitude: '  + position.coords.latitude      + '<br />' +
                        'Longitude: ' + position.coords.longitude     + '<br />' +
                        '<hr />'      + element.innerHTML;

    console.log('Started watching');
}


var onError = function(error) {
    alert('code: '    + error.code    + '\n' +
          'message: ' + error.message + '\n');
}

// get current location
function getPosition(){
 navigator.geolocation.getCurrentPosition(getPositionSuccess, onError);

  }

// update location every specifiy seconds
function watchPosition(watchID){
    window.watchID = navigator.geolocation.watchPosition(watchPositionSuccess, onError, { timeout: 30000 });

}

// clear timeout
function clearWatchPosition(watchID){
  navigator.geolocation.clearWatch(window.watchID);
}

```

**Ionic:**

*Install plugin:*
```sh
$ ionic cordova plugin add cordova-plugin-geolocation --variable GEOLOCATION_USAGE_DESCRIPTION="To locate you"
$ npm install --save @ionic-native/geolocation
```

*Insert into app.module.ts:*
```ts
...

import { Geolocation } from '@ionic-native/geolocation';

...

@NgModule({
  ...

  providers: [
    ...
    Geolocation
    ...
  ]
  ...
})
export class AppModule { }
```

*home.ts:*
```ts
import { Geolocation } from '@ionic-native/geolocation';
import 'rxjs/add/operator/filter'



@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  subscription:any;

  constructor(public navCtrl: NavController,private geolocation: Geolocation) {

  }

// get current position
getPosition(){
  this.geolocation.getCurrentPosition().then((position) => {

    console.log('Latitude: '          + position.coords.latitude          + '\n' +
                'Longitude: '         + position.coords.longitude         + '\n' +
                'Altitude: '          + position.coords.altitude          + '\n' +
                'Accuracy: '          + position.coords.accuracy          + '\n' +
                'Altitude Accuracy: ' + position.coords.altitudeAccuracy  + '\n' +
                'Heading: '           + position.coords.heading           + '\n' +
                'Speed: '             + position.coords.speed             + '\n' +
                'Timestamp: '         + position.timestamp                + '\n');


  }).catch((error) => {
    console.log('Error getting location', error);
  });
}

// update position every specific timeout
watchPosition(){
  this.subscription = this.geolocation.watchPosition({timeout:30000})
                              .filter((p) => p.coords !== undefined) //Filter Out Errors
                              .subscribe(position => {
    console.log('Latitude: '          + position.coords.latitude          + '\n' +
                'Longitude: '         + position.coords.longitude         + '\n' +
                'Altitude: '          + position.coords.altitude          + '\n' +
                'Accuracy: '          + position.coords.accuracy          + '\n' +
                'Altitude Accuracy: ' + position.coords.altitudeAccuracy  + '\n' +
                'Heading: '           + position.coords.heading           + '\n' +
                'Speed: '             + position.coords.speed             + '\n' +
                'Timestamp: '         + position.timestamp                + '\n');

},error=>{
  console.log(error);
})
                              
}

// stop timeout
stopWatchPosition(){
// To stop notifications
this.subscription.unsubscribe()
}

}

```

[Ionic geolocation docs](https://ionicframework.com/docs/native/geolocation/)

More Ionic Native content: [Ionic Native docs](https://ionicframework.com/docs/native/)

<a href="#top">Back to top</a>