# Converting JQM to IONIC
This doc is to convert an app with JQM (**Jquery mobile**) framework to IONIC.
Before starting, you will need to *install ionic, please refer to [https://ionicframework.com/getting-started/](https://ionicframework.com/getting-started/) for more detail guide.*

You also can visit [https://ionicframework.com/docs/](https://ionicframework.com/docs/) to explore more options about the ionic ui framework and api.

# Getting started
Ionic framework is using *HTML* syntax, if you familiar with HTML, it will be easy for you.

After you installed *Ionic*, follow the guide to create a new project with a blank template.

If done, please open your favorite code editor and open the project folder.

Open the *home* folder with the following path:
```sh
src/pages/home
```
This folder will contain your first page of the app. The folder will contain:
1. home.html 
2. home.scss
3. home.ts

The *html* file will the file to write html tag. *Scss* will be the file to style and theming the app. And the *Ts* file will be run the logic of the app with **Angular** syntax (*the latest version now is 4*).


I will start by 

### Header
IONIC header, is located at the top of the **page.html**, the`<ion-header>` tag.
To change from, simply copy header tag or `<h1>` from the JQM `<div data-role="header"></div>` to `<ion-title>`.

Example:
JQM:
```sh
 <div data-role="header">
        <h1>Copy this</h1>
    </div>
```

Ionic:
```sh
<ion-header>
  <ion-navbar>
    <ion-title>
      To here
    </ion-title>
  </ion-navbar>
</ion-header>
```
You can edit the color of the header with:
```sh
<ion-header>
  <ion-navbar color="primary">
    <ion-title>
      To here
    </ion-title>
  </ion-navbar>
</ion-header>
```
Refer to this [doc](https://ionicframework.com/docs/api/components/toolbar/Navbar/) for more customization of header.
