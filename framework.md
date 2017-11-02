## The UI component
### The Header
To start with a header, copy the content from `<div data-role="header">Page Name</div>` tag from your **JQM** project.
And replace the content in `<ion-title>` tag in home.html. Example:

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
```

To **style** the header, choose either `primary`(blue), `secondary`(green), `danger`(red), `light`(light silver) or `dark`(black) class to add into `<ion-navbar>`.
These basic theme are supported by Ionic apps, example:

```sh
<ion-header>
  <ion-navbar color="primary"> 
    <ion-title>
      Page Name
    </ion-title> 
  </ion-navbar>
</ion-header>
```

To **custom** the colors, open `home.scss` file and add:
```sh
$colors: (
  primary:    #488aff, <-- you can modify the color code from here -->
  secondary:  #32db64,
  danger:     #f53d3d,
  light:      #f4f4f4,
  dark:       #222
);
```

To add **icon button** to your header, copy content from `<a>` tag inside the *div header* parent tag.
In your Ionic project, add `<ion-buttons>`, `<button>` and `<ion-icon>` tags inside your `<ion-navbar>` tag, example:

**JQM**:
```sh
<a href="#" data-icon="plus" class="ui-btn-right"></a>
```

**Ionic:**
```sh
<ion-header>
  <ion-navbar color="primary">
    <ion-title>
      Page Name
    </ion-title>
     <ion-buttons end>  <-- end means the right side of the menu, start is left -->
      <button ion-button icon-only>
        <ion-icon name="add"></ion-icon> <-- icon "add" is a plus in Ionic -->
       </button>
    </ion-buttons>
  </ion-navbar>
</ion-header>
```

[Ionic Header Docs](https://ionicframework.com/docs/api/components/toolbar/Header/)
[Ionic scss Theming Docs](https://ionicframework.com/docs/theming/theming-your-app/)

### Footer
For footer, copy the content inside `<div data-role="footer"></div>` from your **JQM** project.
And add `<ion-footer>` below the `<ion-content>` tag in your Ionic project, example:

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

### Buttons
**JQM**: 
```sh
<a href="#" class="ui-btn">Button</a>
<button class="ui-btn">Button</button>
```

**Ionic:**
```sh
<button ion-button>Button</button>
```

[Ionic button docs](https://ionicframework.com/docs/components/#buttons)

### Lists
**JQM**
```sh
<ul data-role="listview">
    <li><a href="#">Acura</a></li>
    <li><a href="#">Audi</a></li>
    <li><a href="#">BMW</a></li>
    <li><a href="#">Cadillac</a></li>
    <li><a href="#">Ferrari</a></li>
</ul>
```

**Ionic:**
```sh
<ion-list>
  <button ion-item>Acura</button>  
  <button ion-item>Audi</button>  
  <button ion-item>BMW</button>  
  <button ion-item>Cadillac</button>  
  <button ion-item>Ferrari</button>  
</ion-list>
```

[Ionic list](https://ionicframework.com/docs/components/#lists)


### Inputs
**JQM**:
```sh
<label for="text-basic">Username:</label>
<input name="text-basic" id="text-basic" value="" type="text">

<label for="password">Password:</label>
<input name="password" id="password" value="" autocomplete="off" type="password">
```

**Ionic:**
```sh
<ion-list>

  <ion-item>
    <ion-label fixed>Username</ion-label>
    <ion-input type="text" value=""></ion-input>
  </ion-item>

  <ion-item>
    <ion-label fixed>Password</ion-label>
    <ion-input type="password"></ion-input>
  </ion-item>

</ion-list>
```

[Ionic input docs](https://ionicframework.com/docs/components/#inputs)


### Radio
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

