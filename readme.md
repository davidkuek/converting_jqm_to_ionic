# Jquery Mobile to Ionic
This readme is for noting down the steps to convert a JQM project to Ionic.

## Getting started
1. Before install Ionic, install nodejs and cordova.
   - [Nodejs](https://nodejs.org/en/download/)
   - [Cordova](https://cordova.apache.org/#getstarted)
   - [Ionic v3](https://ionicframework.com/getting-started/)
2. [Angular v4](https://angular.io/) for your reference of angularjs concept and syntax.
3. Ensure your code editor has **Typescript** package installed.

## After started
After installed Ionic,
1. Create a project
   ```sh
   $ ionic create ProjectName blank
   ```
2. View your project, you can either:
   - Run on your browser (live preview):
   ```sh
   $ cd ProjectName
   $ ionic serve
   ```
   Add `/ionic-lab` to the url `localhost:8100` to view a mobile template.
   - Run on your device (the best way because some feature live preview is not supported).
     Note: Make sure you have Android Studio and Cordova, for iOS will be Xcode
   ```sh
   $ ionic build
   $ ionic cordova run android
   ```
   or
   ```sh
   $ ionic build
   $ ionic cordova run ios
   ```   
   Refer to [deploy docs](https://ionicframework.com/docs/intro/deploying/) for more info.
   

3. Open your project folder with code editor and open the home folder (located in `/src/pages/home`).

    The folder is your home page and it consists:
    - home.html *(app framework)*
    - home.scss *(app styling and theming)*
    - home.ts  *(app function and logic)*

## Note for starter
Some notes before converting a JQM based project to ionic.

1. Jquery are usable in Ionic, however some feature will not be functioning as expected, example:
  - ```$(selector).val()``` getting value or setting value will not able to retrieve value from view.
2. Jquery use for css are still usable.
3. ```document.getElementById``` are not functioning as expected in ionic too, considering using angular data binding.
4. Most **Cordova** functions are still usable in Ionic because phone function in Ionic still rely on **Cordova**, but advised to follow ionic way to use them. 
5. **Success and error handler** for method will changed but the concept and usage will be the same.
6. Function **return** will be to change as well. In Ionic:
  - A function with one return is called **Promise**
  - A function with more than one return is called **Observables**, with more feature as well.
  - A function with no return is called **Void**, you might not need to do anything about it.
7. Jquery **append** is not working as expected as well, use **ngFor** in Angular.
8. **InnerHTML** not usable as well since no.3 is not working.
