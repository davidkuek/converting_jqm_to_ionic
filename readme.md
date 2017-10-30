# Converting JQM to IONIC
This doc is to convert an app with JQM (**Jquery mobile**) framework to IONIC.
Before starting, you will need to install ionic, please refer to [ionic website](https://ionicframework.com/getting-started/) for more detail guide.

You also can visit [ionic docs](https://ionicframework.com/docs/) to explore more options about the ionic ui framework and api.

# Getting started
The common thing between JQM and IONIC is that both are using HTML syntax. If you understand HTML, IONIC framework will be quite simple for you.

After you created a new IONIC project folder, use your code editor and open the ionic folder, under folder:
```sh
src/pages/home
```
will be your home page, with **home.html, home.scss, home.ts**, where html will be your  **Hypertext Markup Language**, scss will be your css and ts will be stand for **typescript** which is similiar to **javascript**.

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
