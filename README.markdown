# jQuery refresh

[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0)

Refresh is a simple jQuery plugin which makes it easy to continuously update selected elements
with data polled from an arbitrary JSON endpoint.

## Usage

Load jQuery and this plugin:

```html
<script type="text/javascript" src="jquery.min.js"></script>
<script type="text/javascript" src="jquery.refresh.js"></script>
```

Next, create appropriate HTML markup and set the `data-id` attribute on the element you want to
refresh:

```html
<div class="status">
  Status of job 3: <span id="job-status" data-id="3">unknown</span>
</div>
```

Let's suppose we have an endpoint at the (relative) URL `/jobs/:id:/status` which returns JSON
objects like the following:

```json
{"id": 42, "status": "pending"}
```

Then, polling and updating the element using this data source can be achieved by setting up
Refresh like this:

```javascript
$("#job-status").refreshJSON("activate", {
  // URL of the JSON endpoint (:id: will be the element's data-id attribute)
  url: "/jobs/:id:/status",

  // refresh interval in milliseconds
  interval: 10000,

  // success callback function receiving the element as context (this) and the JSON data
  success: function(data) {
    // update the element
    $(this).text(data.status);

    if (someCondition) {
      // if you don't want to poll forever
      $(this).refreshJSON("deactivate");
    }
  }
});
```

## License

jQuery Refresh is released under the GNU GPL version 3.
