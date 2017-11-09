# Ionic Native
Usage of phone functions, please have cordova installed before proceed. 

- [SQLite database](#sqlite)
- [Camera](#camera)
- [File](#file)
- [Geolocation](#geolocation)

## <a name="sqlite">Sqlite database
**JQM:**
 ```sh
var dbName = 'Testdb';
var dbVersion = '1.0';
var dbDisplayName = 'Test DB';
var dbSize = 2*1024*1024;
var item_list = []; 


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
 

function updateItem(id,name,desc){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = 'UPDATE ITEM_LIST SET NAME = ?, DESC = ? WHERE ID = ?;';

    db.transaction(function(tx){

        tx.executeSql(query,[name,desc,id],function(tx,result){

            console.log('executed sql:' + result);

        },sqlError);

    },dbError);  

}


function deleteItem(id){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = 'DELETE FROM ITEM_LIST WHERE ID =?;';

    db.transaction(function(tx){

        tx.executeSql(query,[id],function(tx,result){

            console.log('executed sql ' + result);

        },sqlError);

    },dbError);  

}


function addItem(name,desc){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = 'INSERT INTO ITEM_LIST(name,desc) VALUES (?,?);';

    db.transaction(function(tx){

        tx.executeSql(query,[name,desc],function(tx,result){

            console.log('executed sql ' + result);

        },sqlError);

    },dbError);  

}


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


var sqlError = function(err){
    console.log('sql executed error:' + err);
}

var dbError = function(err){
    console.log('db transaction error:' + err);
}
 ```
 
**Ionic:**

*Install plugin:*
 ```sh
$ ionic cordova plugin add cordova-sqlite-storage
$ npm install --save @ionic-native/sqlite
 ```
 
*app.module.ts:*
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

*home.ts:*
```sh
import { SQLite, SQLiteObject } from '@ionic-native/sqlite';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  item_list = [];

  constructor(private sqlite: SQLite) {

  }

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
 
*Note: Sqlite in Ionic is not websql in JQM, therefore is not viewable in debug tools.*

*Note: Sqlite usage may cause your app not viewable with `ionic serve`, therefore view your app device instead.*

[Ionic SQLite Docs](https://ionicframework.com/docs/native/sqlite/)

<a href="#top">Back to top</a>

  

## <a name="camera">Camera
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
*Install the camera plugin:*
```sh
$ ionic cordova plugin add cordova-plugin-camera
$ npm install --save @ionic-native/camera
```

*app.module.ts:*
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

*home.html:*
```sh
  <ion-content padding>
    <img src="{{imageFile}}">
  </ion-content>
```

*home.ts:*
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

<a href="#top">Back to top</a>

## <a name="file">File
**JQM:**

*Creating a new persistent file:*
```sh


function createFile(){
window.requestFileSystem(window.PERSISTENT, 0, function (fs) {

    console.log('file system open: ' + fs.name);
    fs.root.getFile("somePesistentFile.txt", { create: true, exclusive: false }, function (fileEntry) {
        

        console.log(fileEntry.fullPath);
        // fileEntry.name == 'someFile.txt'
        // fileEntry.fullPath == '/someFile.txt'
        
    }, onErrorGetFile);

}, onErrorLoadFs);

}


function createTempFile(){
    window.requestFileSystem(window.TEMPORARY, 5 * 1024 * 1024, function (fs) {

        console.log('file system open: ' + fs.name);

    fs.root.getFile('someTempFile.txt', {create: true, exclusive: true}, function(fileEntry) {
        console.log(fileEntry.fullPath);

    }, onErrorGetFile);

}, onErrorLoadFs);


}


function writeFile(fileEntry, dataObj, isAppend) {

   window.requestFileSystem(window.TEMPORARY, 5*1024*1024, function(fs){

      fs.root.getFile('someTempFile.txt',{create:false}, function(fileEntry) {

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


function readFile() {

   window.requestFileSystem(window.TEMPORARY, 5*1024*1024, function(fs){
      fs.root.getFile('someTempFile.txt', {}, function(fileEntry) {

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


function removeFile() {

   window.requestFileSystem(window.TEMPORARY, 5*1024*1024, function(fs){

      fs.root.getFile('someTempFile.txt', {create: false}, function(fileEntry) {

         fileEntry.remove(function() {
            console.log('File removed.');

         }, onErrorDeleteFile);

      }, onErrorGetFile);

   }, onErrorLoadFs);
}   



    function createDirectory(rootDirEntry) {
    window.requestFileSystem(window.TEMPORARY, 5 * 1024 * 1024, function (rootDirEntry) {        
    rootDirEntry.root.getDirectory('NewDirInRoot', { create: true }, function (dirEntry) {
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
```sh
import { File } from '@ionic-native/file';

  providers: [
    File   
  ]
})
export class AppModule {}
```

*home.ts:*
```sh
import { File } from '@ionic-native/file';


@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  constructor(public navCtrl: NavController,private file: File) {

  }

createFile(){

  let path = this.file.externalRootDirectory;
  let fileName = 'someFile.txt';
  let isAppend = true;
  // true replace file with same name, false returns error

  this.file.createFile(path, fileName,isAppend)
  .then(file => console.log('created' + file.fullPath))
  .catch(err => console.log(err))
  }


writeFile(){

  let path = this.file.externalRootDirectory;
  let fileName = 'someFile.txt';
  let textContent = 'Lorem Ipsum';
  let text = new Blob([textContent],{type:'text/plain'});

  this.file.writeFile(path, fileName, text, {replace:true})
  .then(() => console.log('write success: ' + textContent))
  .catch(err => console.log(err))
}

readFile(){

  let path = this.file.externalRootDirectory;
  let fileName = 'someFile.txt';


  this.file.readAsText(path,fileName)
  .then((result)=>console.log(result))
  .catch(err=> console.log(err))

}

removeFile(){

  let path = this.file.externalRootDirectory;
  let fileName = 'someFile.txt';

  this.file.removeFile(path,fileName)
  .then((result)=>console.log(result))
  .catch(err => console.log(err))
}


createDir(){

  let path = this.file.externalRootDirectory;
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
```sh
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


function getPosition(){
 navigator.geolocation.getCurrentPosition(getPositionSuccess, onError);

  }


function watchPosition(watchID){
    window.watchID = navigator.geolocation.watchPosition(watchPositionSuccess, onError, { timeout: 30000 });

}

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
```sh
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
```sh
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

stopWatchPosition(){
// To stop notifications
this.subscription.unsubscribe()
}

}

```

[Ionic geolocation docs](https://ionicframework.com/docs/native/geolocation/)

More Ionic Native content: [Ionic Native docs](https://ionicframework.com/docs/native/)

<a href="#top">Back to top</a>