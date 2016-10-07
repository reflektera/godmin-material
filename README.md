#### Godmin [![Gem Version](http://img.shields.io/gem/v/godmin.svg)](https://rubygems.org/gems/godmin)

# Godmin Material

This is a fork of the Godmin admin framework with the purpose of implementing Material Design through the Angular Material framework in Godmin without disrupting the automatic view generation. Angular is only used to bootstrap and include Angular Material. We include the libraries via CDN now but this will hopefully be changed to use a package manager such as npm in the future.


## Installation

- Include Godmin-Material in your Gemfile: `gem "godmin", github: "inserve/godmin-material", branch: "master"`
- If you haven't already, change your `application.css` to `application.scss`
  - Add these two lines to your `application.scss`:

    ```
      @import "godmin/variables";
      @import "godmin/index";
    ```
- Run `bundle`
- Start your Rails app and try out your fresh materialistic admin interface!

---

## Configuration

### SASS color overrides

All the SASS variables can be found in [app/assets/stylesheets/godmin/variables.scss](https://github.com/inserve/godmin-material/tree/master/app/assets/stylesheets/godmin/variables.scss)

and you can override them like so:

- Create or copy the Godmin-Material variables.scss inside /yourapp/app/assets/stylesheets/

`in /yourapp/app/assets/stylesheets/application.scss`

```
  @import "variables";
  @import "godmin/index";
```

You can now override any of the given variables in your own local `variables.scss` and refresh the admin interface to see the reflected changes.

Notes:
- if your application.scss file is a .css simply rename it to .scss
- if you already have `*= require godmin` at the top in your application.scss remove it now, we include it via SASS to have control of the order it gets loaded

---

## Components

### Async search to set related ID

This component requires a custom written `GET` action in your backend alongside the related data being presented via your `@resource` into the view you're searching in.
Documentation for examples of this is pending.

In your view add this markup

```
  <div ng-app="godmin">
    <search
      url="/path/to/api/get-request?q="
      default-query="<%= @resource.related_resource ? @resource.related_resource.name : '' %>"
      hidden-name="account[contact_id]"
      first-key="firstname"
      second-key="lastname" />
  </div>
```

| Attribute name  | Value specification                                                                                                                                                       |
|---------------- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------  |
| url             | string, url to the api get route                                                                                                                                          |
| default-query   | This can be anything from a default value to, prefferably and as the example here shows, the value from the @resource provided via the resource service                   |
| hidden-name     | the name for the hidden input, this should be resource_name[column_name], see example above                                                                                                  |
| first-key       | the first key for the related resource to show, for example first-key='firstname' would result in the displayed value in the results will be related_resource.firstname   |
| second-key      | see first-key, never use this without first setting the above

### Dialog

If you require dialogs (modals) in your custom CRUD views you can write a Dialog Component:

```
  <div style="visibility: hidden">
    <div class="md-dialog-container" id="myDialogID">
      <md-dialog layout-padding>
        <md-dialog-content>
          <!-- Dialog body -->
        </md-dialog-content>
        <md-dialog-actions>
          <!-- hide() hides the currently open Dialog (same as clicking outside) -->
          <md-button ng-click="hide()">
            Close
          </md-button>
        </md-dialog-actions>
      </md-dialog>
    </div>
  </div>
```

To have a trigger for the dialog simply place a button wherever you want it with this markup:

```
  <md-button ng-click="showDialog($event, '#myDialogID')">
    Open Dialog
  </md-button>
```

---


#### for further help check [Godmins' official documentation](https://github.com/varvet/godmin)