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
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
var query = 'CREATE TABLE IF NOT EXISTS ITEM_LIST ' +  
            '([id] INTEGER PRIMARY KEY AUTOINCREMENT, [name] TEXT,[desc] TEXT);';

    db.transaction(function(tx){
        tx.executeSql(query, [],function(tx,result){
            console.log('executed Sql:' + result);
        },function(err){
            console.log('SQL executed error ' + err);
        });
    },
    function(err){
      console.log('create database error ' + err)
    });
}
 

function updateItem(id,name,desc){
    var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
  var query = 'UPDATE ITEM_LIST SET NAME = ?, DESC = ? WHERE ID = ?;';

    db.transaction(function(tx){
        tx.executeSql(query,[name,desc,id],function(tx,result){
            console.log('executed sql:' + result)
        },function(err){
            console.log('SQL executed error ' + err);
        })
    },
    function(err){
      console.log('update item error ' + err)
    });  
}

function deleteItem(id){
    var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
  var query = 'DELETE FROM ITEM_LIST WHERE ID =?;';

    db.transaction(function(tx){
        tx.executeSql(query,[id],function(tx,result){
            console.log('executed sql ' + result);
        },function(err){
            console.log('SQL executed error ' + err);
        })
    },
    function(err){
      console.log('delete item error ' + err)
    });  
}


function addItem(name,desc){
var db = window.openDatabase(dbName, dbVersion, dbDisplayName, dbSize);
  var query = 'INSERT INTO ITEM_LIST(name,desc) VALUES (?,?);';

    db.transaction(function(tx){
        tx.executeSql(query,[name,desc],function(tx,result){
            console.log('executed sql ' + result);
        },function(err){
            console.log('SQL executed error' + err);
        })
    },
    function(err){
      console.log('add item error ' + err)
    });  
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

## File
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
import { File } from '@ionic-native/file'


constructor(private file: File) { }


createFile(){

  this.file.createFile(dirEntry, fileName,isAppend)
  .then(() => console.log('created'))
  .catch(err => console.log(err))
  }



createDirectory(){
  this.file.createDir(dirEntry, dirName, isAppend)
  .then(()=> console.log('directory created.'))
  .catch(err=> console.log(err))
}

}
```

[Ionic file docs](https://ionicframework.com/docs/native/file/)

## Geolocation
**JQM:**
```sh

function getPosition(){
 navigator.geolocation.getCurrentPosition(onSuccess, onError);
    var onSuccess = function(position) {
        alert('Latitude: '          + position.coords.latitude          + '\n' +
              'Longitude: '         + position.coords.longitude         + '\n' +
              'Altitude: '          + position.coords.altitude          + '\n' +
              'Accuracy: '          + position.coords.accuracy          + '\n' +
              'Altitude Accuracy: ' + position.coords.altitudeAccuracy  + '\n' +
              'Heading: '           + position.coords.heading           + '\n' +
              'Speed: '             + position.coords.speed             + '\n' +
              'Timestamp: '         + position.timestamp                + '\n');
    };

    // onError Callback receives a PositionError object
    //
    function onError(error) {
        alert('code: '    + error.code    + '\n' +
              'message: ' + error.message + '\n');
    }
  }

   

function watchPosition(watchID){
    watchID = navigator.geolocation.watchPosition(onSuccess, onError, { timeout: 30000 });
    // Options: throw an error if no update is received every 30 seconds.
    //
        function onSuccess(position) {
        var element = document.getElementById('geolocation');
        element.innerHTML = 'Latitude: '  + position.coords.latitude      + '<br />' +
                            'Longitude: ' + position.coords.longitude     + '<br />' +
                            '<hr />'      + element.innerHTML;
        }

    // onError Callback receives a PositionError object
    //
        function onError(error) {
          alert('code: '    + error.code    + '\n' +
              'message: ' + error.message + '\n');
        }

}

function clearWatchPosition(watchID){
  navigator.geolocation.clearWatch(watchID);
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

...

constructor(private geolocation: Geolocation) {}

...

getPosition(){
  this.geolocation.getCurrentPosition().then((resp) => {

    console.log(resp.coords.latitude);
    console.log(resp.coords.longtitude);
    console.log(resp.coords.altitude);
    console.log(resp.coords.accuracy);
    console.log(resp.coords.altitudeAccuracy);
    console.log(resp.coords.heading);
    console.log(resp.coords.speed);
    console.log(resp.coords.timestamp);

  }).catch((error) => {
    console.log('Error getting location', error);
  });
}

let watch = this.geolocation.watchPosition();
watch.subscribe((data) => {
 // data can be a set of coordinates, or an error (if an error occurred).
 // data.coords.latitude
 // data.coords.longitude
});
```

[Ionic geolocation docs](https://ionicframework.com/docs/native/geolocation/)

