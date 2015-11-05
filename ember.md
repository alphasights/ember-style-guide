# Ember Best Practices

This is a collection of best practices we've found useful when developing Ember
applications at AlphaSights. You're incouraged to follow them.

## Official Guide

Read the [official guide](http://guides.emberjs.com/v2.1.0/).

## Table Of Contents

+ [Genera](#general)
+ [Actions](#actions)
+ [Ember Data](#ember-data)
+ [Router](#router)
+ [Pods](#pods)
+ [Templates](#templates)
+ [Styles](#styles)

## General

Use [computed properties](http://guides.emberjs.com/v2.1.0/object-model/computed-properties/) whenever applicable.

---

Use `Ember.computed.oneWay` instead of `Ember.computed.alias` unless there is a
specific reason for propagating changes back to the source.

---

Prefer using the `on` syntax for events like `didInsertElement` instead of
overriding the method directly. This spares you from having to call `super` and
gives you a chance to give a meaningful name to the method.

**Do this:**

```javascript
setupFoundation: Ember.on('didInsertElement', function() {
  Ember.$(document).foundation({ dropdown: {} });
}),
```

**Don't do this:**

```javascript
didInsertElement: function() {
  this._super.apply(this, arguments);
  Ember.$(document).foundation({ dropdown: {} });
}
```

## Actions

Use camel case for action properties.

**Do this:**

```
{{as-star-project model=project onSave=(action "saveProject")}}
```

**Don't do this:**

```
{{as-star-project model=project onsave=(action "saveProject")}}
```

---

Use closure actions whenever applicable.

**Prefer**

```
<!-- template.hbs -->
{{as-star-project model=project onSave=(action "saveProject")}}

<!-- as-star-project.hbs -->
<button {{action this.attrs.onSave}}>Save</button>
```

**Over**

```
<!-- template.hbs -->
{{as-star-project model=project onSave="saveProject"}}

<!-- as-star-project.hbs -->
<button {{action "save"}}>Save</button>

<!-- as-star-project.js -->
Ember.Component.extend({
  actions: {
    save: function() {
      this.sendAction('onSave');
    }
  }
});
```

---

When using closure actions, access the passed closure using `this.attrs`

```
<!-- template.hbs -->
{{as-rate-project model=project onRate=(action "rateProject")}}

<!-- as-rate-project.hbs -->
<input type="text" oninput={{action "rate" value="target.value"}} />

<!-- as-star-project.js -->
Ember.Component.extend({
  actions: {
    rate: function(value) {
      this.attrs.onSave(value);
    }
  }
});
```

## Ember Data

Use the appropriate method to retrieve data:

| Type          | Async from server/store | Sync from store      | Query server               |
|---------------|-------------------------|----------------------|----------------------------|
| Single Record | findRecord(type,id)     | peekRecord(type, id) | queryRecord(type, {query}) |
| All Records   | findAll(type)           | peekAll(type)        | query(type, {query})       |

## Router

Pretty much everything apart from components has to be laid out based on the router structure, e.g.:

```javascript
Router.map(function() {
  this.route('dashboard', { path: '/' });
  this.route('performance');
  this.route('projects');

  this.route('team', function() {
    this.route('team.project', { path: ':project_id' });
  });

  this.route('application_error', { path: '*path' });
});
```

## Pods

Use pods. Every pod should follow this structure:

```
app/pods/projects/controller.js
app/pods/projects/route.js
app/pods/projects/template.hbs
```

## Templates

Use double quotes for strings.

---

Whenever you need a wrapper for a certain element, avoid creating a class name
like `element-wrapper`. Instead, add the element class to the wrapper element
and have an anonymous element inside.

**Do this:**

```html
<div class="message">
  <div>
  </div>
</div>
```

**Don't do this:**

```html
<div class="message-wrapper">
  <div class="message">
  </div>
</div>
```

---

Use a single line when the parameter list is short.

**Do this:**

```
{{as-star-project model=project onSave=(action "saveProject")}}
```

**Don't do this:**

```
{{as-star-project
  model=project
  onSave=(action "saveProject")}}
```

---

Use "Clojure" style formatting when the parameter list is very long.

**Do this:**

```
{{as-quick-jump-result-content
  title=name
  details=accountName
  resourceId=id
  resourcePath="client/contacts"}}
```

**Don't do this:**

```
{{
  as-quick-jump-result-content
  title=name
  details=accountName
  resourceId=id
  resourcePath="client/contacts"
}}
```

---

Use `.` as a separator for the Ember resolver. Use `/` only for templates.

**Do this:**

```
export default Ember.Component.extend({
  layoutName: 'components/as-widget/widget',
});
```

**Don't do this:**

```
export default Ember.Component.extend({
  layoutName: 'components.as-widget.widget',
});
```

## Styles

Prefix global variable names with the file/directory name, i. e. if you're
adding a variable to `templates/team/_project.scss`, make sure to prefix it with
`team-project`.

**Do this:**

`$team-project-header-height: rem-calc(40);`

**Don't do this:**

`$header-height: rem-calc(40);`

---

If you have to handle optional classes for a certain selector, put the styles for those at the end.

**Do this:**

```scss
.project-list-item {
  padding: 5px;

  > div {
    color: white;
  }

  &.no-target {
    background-color: red;
  }
}
```

**Don't do this:**

```scss
.project-list-item {
  padding: 5px;

  &.no-target {
    background-color: red;
  }

  > div {
    color: white;
  }
}
```
