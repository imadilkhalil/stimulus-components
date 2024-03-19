---
title: Rails Autosave
description: A Stimulus controller to autosubmit Rails forms.
package: rails-autosave
packagePath: 'stimulus-rails-autosave'
---

## Installation

:installation-block{:package="package" :packagePath="packagePath" controllerName="autosave"}

## Usage

::code-block{tabName="app/views/todos/edit.html.erb"}

```erb
<%= form_with model: @todo, data: { controller: 'autosave' } do |f| %>
  <div class="field">
    <%= f.label :description %>

    <!-- With custom event! -->
    <%= f.text_field :description, data: { action: 'keyup->autosave#save' } %>
  </div>

  <div class="field">
    <%= f.label :completed %>
    <%= f.check_box :completed, data: { action: 'autosave#save' } %>
  </div>

  <%= f.submit %>
<% end %>
```

::

## Configuration

| Attribute                   | Default | Description                                                   | Optional |
| --------------------------- | ------- | ------------------------------------------------------------- | -------- |
| `data-autosave-delay-value` | `150`   | Delay (in ms) before actually submit the form. (0 to disable) | ✅       |

## Extending Controller

::extending-controller
::code-block{tabName="app/javascript/controllers/rails_autosave_controller.js"}

```js
import Autosave from 'stimulus-rails-autosave'

export default class extends Autosave {
  static values = {
    delay: {
      type: Number,
      default: 1000, // You can change the default delay here.
    },
  }

  connect() {
    super.connect()
    console.log('Do what you want here.')
  }
}
```

::
::
