Inline JavaScript, which is used for framework plugins and widgets (e.g., slideshows, events, tabs, etc.), should be wrapped in the following code:
```html
<script>
  window.addEventListener('inlineJSReady', function() {
    // Your JavaScript goes here.
  }, false);
</script>
```

# Audio/Video Players
We suggest that you make use of the media hosting service [MediaHub](https://mediahub.unl.edu/), which provides embed codes that integrate some very useful accessibly features such as searchable captions. Media hosted outside of MediaHub can still use the same player as follows.

To embed a video on your page so that it will work across browsers, use the `mediaelement_wdn` plugin. To use this plugin, you will need to do the following:

1. Embed the video on your page with either the `<audio>` or the `<video>` element.
2. Give the `<audio>` or the `<video>` element a class of `wdn_player`.
    * [learn more about the audio element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)
    * [learn more about the video element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video)
3. Load the `mediaelement_wdn` plugin with `<script>WDN.initializePlugin('mediaelement_wdn');</script>`. Please note: You only need to run this script once per page. Putting it at the bottom of your content ensure that all players get loaded when ready.

There are many things to consider when it comes to accessibility and media.
1. All media must have captions. [UNL MediaHub](http://mediahub.unl.edu/) makes this easy.
2. Avoid auto-playing media: Media that automatically plays when a page is loaded can be confusing and unwanted.
3. Keep flashes of light to a minimum. Excessive flashes and/or strobing effects can cause issues for people who are prone to seizures.

Media should be hosted on the unl.edu domain whenever possible (as opposed to [YouTube](https://www.youtube.com/), etc.) to ensure that it is available to all visitors. Some locations such as China or K–12 schools will block popular media hosting platforms such as [YouTube](https://www.youtube.com/) or [Vimeo](https://vimeo.com/). To ensure that everyone who visits your site can watch media, please host the content on unl.edu. An easy solution for hosting media at UNL is [UNL MediaHub](http://mediahub.unl.edu/).

# Button Toggles

Button Toggles allow buttons to toggle other elements when clicked. This component is the base for other components. This component rely on specific CSS classes and does have CSS animations that will take place during the toggling.

| Options  | Data Attribute | Default value |Description |
| -------- | -------------- | ----------- | ------ |
| Controls | `data-controls`  | `''` |This will be the id of the element that we are going to toggle (required) |
| Label On | `data-label-on` | `''` | This will control the aria label for the button for when the element is off/collapsed, not needed if there is text inside the button |
| Label Off | `data-label-off` | `''` | This will control the aria label for the button for when the element is on/expanded, not needed if there is text inside the button |
| Start Expanded | `data-start-expanded` | `'true'` | This will allow us to define the starting state of the toggle, this should be pared with the `hidden` attribute on the toggled element to avoid bad content paints before the javascript loads |

| Events | Dispatches/Listens | Description |
| ------ | ------------------ | ----------- |
| `toggleButtonOn` | Dispatches | This event is dispatched when the button is toggled to the on/expanded state |
| `toggleButtonOff` | Dispatches | This event is dispatched when the button is toggled to the off/collapsed state |
| `toggleElementOn` | Dispatches | This event is dispatched when the element is toggled to the on/expanded state |
| `toggleElementOff` | Dispatches | This event is dispatched when the element is toggled to the off/collapsed state |
| `commandClose` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button off/collapsed |
| `commandOpen` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button on/expanded |
| `commandToggle` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button state |

| Keys | Actions |
| ---- | ------- |
| `space` | Toggles the state |
| `escape` | Tries to toggle off/collapsed |

_These keys only work when focus is on the button_

```html
<!-- Starting Expanded Example -->
<div id="my-div">
  My First Div
</div>

<button
  class="dcf-btn-toggle dcf-btn dcf-btn-primary"
  data-controls="my-div"
  data-label-on="Open My First Div"
  data-label-off="Close My First Div"
  data-start-expanded="true"
>
  Toggle My First Div (Starts On)
</button>

<!-- This is only required once per page with button-toggles -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('button-toggles');
  }, false);
</script>
```

```html
<!-- Starting Collapsed Example -->
<div id="my-div-with-id" hidden>
  My Second Div
</div>

<button
  id="my-div-with-id-toggle-button"
  class="dcf-btn-toggle dcf-btn dcf-btn-primary"
  data-controls="my-div-with-id"
  data-label-on="Open My Second Div"
  data-label-off="Close My Second Div"
  data-start-expanded="false"
>
  Toggle My Second Div (Starts Off)
</button>

<!-- This is only required once per page with button-toggles -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('button-toggles');
  }, false);
</script>
```

# Card As Link

Card as link will allow cards to be a clickable link with the link defined by `dcf-card-link`. This component rely on specific CSS classes.

| Events | Dispatches/Listens | Description |
| ------ | ------------------ | ----------- |
| `mousedown` | Listens | When the mouse is pressed down a timer starts |
| `mouseup` | Listens | When the mouse is released and the timer is within 200 milliseconds then the link will be clicked |

```html
<!-- Example Card as Link -->
<div class="dcf-card dcf-card-as-link dcf-d-flex dcf-flex-col">
  <div class="dcf-card-block dcf-2nd">
    <h2><a class="dcf-card-link" href="https://www.unl.edu/">Church-key ennui gastropub</a></h2>
    <p>Sriracha Etsy XOXO street art, chillwave 8-bit hoodie <abbr>VHS</abbr> blog Pitchfork authentic paleo ethical messenger bag. Raw denim Blue Bottle flannel Carles Williamsburg narwhal, cray drinking vinegar messenger bag gluten-free twee ugh. <a href="https://www.google.com/">Here's another link</a></p>
  </div>
  <div class="dcf-ratio dcf-ratio-16x9 dcf-1st">
    <img
      class="dcf-ratio-child dcf-obj-fit-cover dcf-h-100% dcf-w-100%"
      sizes="(min-width: 41.956em) 43vw, 88vw"
      srcset="wdn/templates_5.3/images/dev/150821-tunnel-325-sm-min.jpg 284w,
  wdn/templates_5.3/images/dev/150821-tunnel-325-md-min.jpg 505w,
  wdn/templates_5.3/images/dev/150821-tunnel-325-lg-min.jpg 898w,
  wdn/templates_5.3/images/dev/150821-tunnel-325-xl-min.jpg 1596w"
      src="data:image/gif;base64,R0lGODlhAQABAAAAADs="
      alt="">
  </div>
</div>

<!-- This is only required once per page with card as link -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('card-as-link');
  });
</script>
```


# Collapsible Field Set

Collapsible field set's are field sets that can be collapsed. This will add a toggle button in the legend and allow the contents within the field set to be collapsible. This component builds on the button toggles component. This component rely on specific CSS classes and does have CSS animations that will take place during the toggling.

Items inside the fieldset tag will be moved into an internal div tag which is used for the collapsing of the content. This will result in event listeners and other javascript variables to not work since the original elements would be deleted. As a result there is a `fieldsetReady` event that is fired after this process takes place, so any event listeners or variables will need to be re-created after the event has been dispatched.

| Options  | Data Attribute | Default value |Description |
| -------- | -------------- | ----------- | ------ |
| Start Expanded | `data-start-expanded` | `'true'` | This will allow us to define the starting state of the toggle, this should be pared with the `hidden` attribute on the toggled element to avoid bad content paints before the javascript loads |

| Events | Dispatches/Listens | Description |
| ------ | ------------------ | ----------- |
| `toggleButtonOn` | Dispatches | This event is dispatched when the button is toggled to the on/expanded state |
| `toggleButtonOff` | Dispatches | This event is dispatched when the button is toggled to the off/collapsed state |
| `toggleElementOn` | Dispatches | This event is dispatched when the element is toggled to the on/expanded state |
| `toggleElementOff` | Dispatches | This event is dispatched when the element is toggled to the off/collapsed state |
| `commandClose` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button off/collapsed |
| `commandOpen` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button on/expanded |
| `commandToggle` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button state |
| `fieldsetReady` | Dispatches | Once the fieldset is ready and initialized this event will be dispatched |

| Keys | Actions |
| ---- | ------- |
| `space` | Toggles the state |
| `escape` | Tries to toggle off/collapsed |

_These keys only work when focus is on the button_

```html
<!-- Starts Expanded Example -->
<form class="dcf-form">
  <fieldset class="dcf-collapsible-fieldset">
    <legend>Checkboxes</legend>
    <div class="dcf-input-checkbox">
      <input id="dcf-components-form-checkbox1A" type="checkbox" value="0">
      <label for="dcf-components-form-checkbox1A">Checkbox 1</label>
    </div>
    <div class="dcf-input-checkbox">
      <input id="dcf-components-form-checkbox2A" type="checkbox" value="1">
      <label for="dcf-components-form-checkbox2A">Checkbox 2</label>
    </div>
  </fieldset>
</form>

<!-- This is only required once per page with collapsible fieldset -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('collapsible-fieldsets');
  }, false);
</script>
```

```html
<!-- Starts Collapsed Example -->
<form class="dcf-form">
  <fieldset class="dcf-collapsible-fieldset" data-start-expanded="false" hidden>
    <legend>Checkboxes (Starts collapsed)</legend>
    <div class="dcf-input-checkbox">
      <input id="dcf-components-form-checkbox1B" type="checkbox" value="0">
      <label for="dcf-components-form-checkbox1B">Checkbox 1</label>
    </div>
    <div class="dcf-input-checkbox">
      <input id="dcf-components-form-checkbox2B" type="checkbox" value="1">
      <label for="dcf-components-form-checkbox2B">Checkbox 2</label>
    </div>
  </fieldset>
</form>

<!-- This is only required once per page with collapsible fieldset -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('collapsible-fieldsets');
  }, false);
</script>
```

# Events
Pulling data from the [UNL Events](https://events.unl.edu/) system is available with a number of widgets, each with their own styling and interactions.

The `events` plugin provides a vertically rendered list of upcoming events. The `monthwidget` plugin provides a tabular month calendar rendering of events for the current month. The `events-band` plugin provides a horizontal block grid of upcoming events. Each of these plugins work by providing a placeholder element on your page and adding a script to inject the content loaded asynchronously from the events system.

### How to Configure the Widgets
All of the events widgets are initialized via JavaScript with the `WDN.initializePlugin('plugin-name', {configuration object})` function. A JavaScript object can be passed as the second parameter to customize the widgets.

For example, all of the widgets will use the main UNL calendar by default, but you can use your calendar by passing a `url` option in the configuration object (the second parameter of the `WDN.initializePlugin function)`. Note that the `url` option has to be the base URL for your calendar (use https://events.unl.edu/yourcalendar/ and not https://events.unl.edu/yourcalendar/upcoming). For example:
```html
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('events', {url: 'https://events.unl.edu/yourcalendar/', limit: 5});
  });
</script>
```

## Events Month Widget
| Options     | Type     | Default                     | Description                                        |
| ------------|----------|-----------------------------|----------------------------------------------------|
| `url`       | String   | `'https://events.unl.edu/'` | URL of the events calendar you'd like to pull from |
| `container` | Selector | `'#monthwidget'`            | A CSS selector for loading the widget into         |  

```html
<div id="monthwidget"></div>
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('monthwidget');
  });
</script>
```

## Events List Widget
| Options     | Type     | Default                     | Description                                                 |
| ------------|----------|-----------------------------|-------------------------------------------------------------|
| `url`       | String   | `'https://events.unl.edu/'` | URL of the events calendar you'd like to pull from          |
| `title`     | String   | `''`                        | Label for the _More Events_ link                            |
| `container` | Selector | `'#wdn_calendarDisplay'`    | A CSS selector for loading the widget into                  |
| `limit `    | Integer  | `10`                        | Maximum number of upcoming events to show                   |
| `rooms `    | Boolean  | `false `                    | A flag to designate if event location rooms should be shown |

```html
<div id="events"></div>
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('events', {limit: 5});
  });
</script>
```

## Events Band Widget
| Options     | Type     | Default                     | Description                                                 |
| ------------|----------|-----------------------------|-------------------------------------------------------------|
| `url`       | String   | `'https://events.unl.edu/'` | URL of the events calendar you'd like to pull from          |
| `title`     | String   | `''`                        | Label for the _More Events_ link                            |
| `container` | Selector | `'#events-band'`            | A CSS selector for loading the widget into                  |
| `limit `    | Integer  | `10`                        | Maximum number of upcoming events to show                   |
| `rooms `    | Boolean  | `false `                    | A flag to designate if event location rooms should be shown |

```html
<div id="events-band"></div>
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('events-band', {limit: 6, rooms: true});
  });
</script>
```

# Extended Fonts
To load the optional brand serif font (Source Serif), apply the `unl-font-serif` class to desired text, then add this snippet of JavaScript to either your page or your site's JavaScript:

```html
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('font-serif');
  }, false);
</script>
```

# Figcaption Toggles

Figcaption toggles allow figure captions to be toggles visible. This component builds off the button toggles. This component rely on specific CSS classes and does have CSS animations that will take place during the toggling.

| Events | Dispatches/Listens | Description |
| ------ | ------------------ | ----------- |
| `toggleButtonOn` | Dispatches | This event is dispatched when the button is toggled to the on/expanded state |
| `toggleButtonOff` | Dispatches | This event is dispatched when the button is toggled to the off/collapsed state |
| `toggleElementOn` | Dispatches | This event is dispatched when the element is toggled to the on/expanded state |
| `toggleElementOff` | Dispatches | This event is dispatched when the element is toggled to the off/collapsed state |
| `commandClose` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button off/collapsed |
| `commandOpen` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button on/expanded |
| `commandToggle` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button state |
| `fieldsetReady` | Dispatches | Once the fieldset is ready and initialized this event will be dispatched |

| Keys | Actions |
| ---- | ------- |
| `space` | Toggles the state |
| `escape` | Tries to toggle off/collapsed |

_These keys only work when focus is on the button_

```html
<!-- Figcaption Toggles Example -->
<figure>
  <div class="dcf-ratio dcf-ratio-16x9 dcf-ratio-1x1@sm dcf-ratio-16x9@lg">
    <img class="dcf-d-block dcf-ratio-child dcf-obj-fit-cover" src="wdn/templates_5.3/images/dev/150821-tunnel-325-xl-min.jpg" alt="">
  </div>
  <figcaption class="dcf-figcaption dcf-figcaption-toggle">
    Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum.
    <small class="dcf-txt-xs dcf-txt-nowrap">Illustration by Jane Doe</small>
  </figcaption>
</figure>

<!-- This is only required once per page with figcaption toggles -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('figcaption-toggles');
  }, false);
</script>
```

# Gallery

Gallery is way to showcase images on a page. Added the `dcf-gallery-img` will allow the action of click on the image to open a modal with a carousel of other images to click through. This component builds off the modal component.

| Options  | Data Attribute | Default value |Description |
| -------- | -------------- | ----------- | ------ |
| Cutline | `data-cutline` | `''` | This will display a formatted cutline on image in the modal |
| Credit | `data-credit` | `''` | This will display formatted credit text on image in the modal |

```html
<!-- Gallery Example -->
<img class="dcf-gallery-img" src="/images/test_320.jpg" alt="Placeholder image." data-cutline="Cras justo odio, dapibus ac facilisis in, egestas eget quam." data-credit="Photo by Jane Doe">
<img class="dcf-gallery-img" src="/images/test_480.jpg" alt="Placeholder image.">
<img class="dcf-gallery-img" src="/images/test_600.jpg" alt="Placeholder image.">
<img class="dcf-gallery-img" src="/images/test_768.jpg" alt="Placeholder image." data-cutline="asdasdada" data-credit="asdasdad">
<img class="dcf-gallery-img" src="/images/test_1040.jpg" alt="Placeholder image.">
<img class="dcf-gallery-img" src="/images/test_320.jpg" alt="Placeholder image.">
<img class="dcf-gallery-img" src="/images/test_480.jpg" alt="Placeholder image." data-cutline="asdasdada" data-credit="asdasdad">
<img class="dcf-gallery-img" src="/images/test_600.jpg" alt="Placeholder image.">
<img class="dcf-gallery-img" src="/images/test_768.jpg" alt="Placeholder image.">
<img class="dcf-gallery-img" src="/images/test_1040.jpg" alt="Placeholder image." data-cutline="asdasdada" data-credit="asdasdad">
<img class="dcf-gallery-img" src="/images/test_320.jpg" alt="Placeholder image.">
<img class="dcf-gallery-img" src="/images/test_480.jpg" alt="Placeholder image.">

<!-- This is only required once per page with a gallery -->
<script>
  window.addEventListener('inlineJSReady', function() {
      WDN.initializePlugin('gallery');
  }, false);
</script>
```

# GSAP
Framework animations use [GreenSock Animation Platform](https://greensock.com/docs/) (GSAP) version 3.x. You can use framework classes for [scroll animations](https://wdn.unl.edu/documentation/5.0/css/unl-specific#scroll-animations) or create your own custom animations by beginning with the following JavaScript:

```html
<script>
  window.addEventListener('DOMContentLoaded', function() {
    require(['plugins/gsap/gsap.min'], function() {
      // Custom GSAP goes here
    });
  }, false);
</script>
```

# Modal

Modals are similar to the new dialog tags but this was made long before the dialog tag was implemented in browsers. This component rely on specific CSS classes.

This component is baked into the WDN framework since it is almost always loaded on every page for the UNL Search. As a result the plugin for this component does not need to initialized manually since it will automatically be loaded on page load.

We can have multiple buttons which controls a single modal. Only one modal can be opened at a time.

| Options  | Data Attribute | Description |
| -------- | -------------- | ------ |
| Toggles Modal | `data-toggles-modal`| This option can be set on the buttons which toggles the modal. This lets us know which modal to toggle when the button is clicked |
| Deliberate Close Only | `data-deliberate-close-only` | This option can be set on the modal element. This will prevent the user from being able to click the overlay to close the modal |
| Confirm Close | `data-confirm-close` | This option can be set on the modal element. If it is not empty it will ask the user to confirm the closing of the modal. The confirmation's text will be the contents of this data attribute |

| Events | Dispatches/Listens | Data Detail | Description |
| ------ | ------------------ | ----------- | ---------- | 
| `ModalPreOpenEvent_${modalId}` | Dispatches | `btn`: the button that was used to open the modal | Before a modal is opened this custom event will be dispatched on the document object. `modalId` will be the ID of the modal being opened |
| `ModalOpenEvent_${modalId}` | Dispatches | | When a modal is opened this custom event will be dispatched on the document object. `modalId` will be the ID of the modal being opened |
| `ModalPreCloseEvent_${modalId}` | Dispatches | | Before a modal is closed this custom event will be dispatched on the document object. `modalId` will be the ID of the modal being opened |
| `ModalCloseEvent_${modalId}` | Dispatches | | When a modal is closed this custom event will be dispatched on the document object. `modalId` will be the ID of the modal being opened |

| Keys | Actions |
| ---- | ------- |
| `escape` | If the modal is open it will close it |

```html
<!-- Example Modal -->
<button class="dcf-btn dcf-btn-primary dcf-btn-toggle-modal" data-toggles-modal="test-modal-1" type="button" disabled>Toggle Modal 1</button>
<div class="dcf-modal" id="test-modal-1" hidden>
  <div class="dcf-modal-wrapper">
    <div class="dcf-modal-header">
      <h3>Example Modal 1</h3>
      <button class="dcf-btn-close-modal">Close</button>
    </div>
    <div class="dcf-modal-content">
      <p>...</p>
      <button class="dcf-btn dcf-btn-primary dcf-btn-toggle-modal" data-toggles-modal="test-modal-1" type="button" disabled>Toggle Modal 1</button>
      <button class="dcf-btn dcf-btn-primary dcf-btn-toggle-modal" data-toggles-modal="test-modal-2" type="button" disabled>Toggle Modal 2</button>
    </div>
  </div>
</div>

<button class="dcf-btn dcf-btn-primary dcf-btn-toggle-modal" data-toggles-modal="test-modal-2" type="button" disabled>Toggle Modal 2</button>
<div class="dcf-modal" id="test-modal-2" hidden>
  <div class="dcf-modal-wrapper">
    <div class="dcf-modal-header">
      <h3>Example Modal 2</h3>
      <button class="dcf-btn-close-modal">Close</button>
    </div>
    <div class="dcf-modal-content">
      <p>...</p>
      <button class="dcf-btn dcf-btn-primary dcf-btn-toggle-modal" data-toggles-modal="test-modal-1" type="button" disabled>Toggle Modal 1</button>
      <button class="dcf-btn dcf-btn-primary dcf-btn-toggle-modal" data-toggles-modal="test-modal-2" type="button" disabled>Toggle Modal 2</button>
    </div>
  </div>
</div>
```

# Popup

Popups are similar to some frameworks tooltips or the native browser popovers. This component will display a block of html relative to a button. This component is build off of the toggle button component. This component rely on specific CSS classes and does have CSS animations that will take place during the toggling.

This component is baked into the WDN framework since it is almost always loaded on every page for the visit/apply/give buttons. As a result the plugin for this component does not need to initialized manually since it will automatically be loaded on page load.

The popup will close if you click outside the popup element's area. Only one popup can be open at a time. This component can be nested so you can have popups inside other popups.

| Options  | Data Attribute | Default value | Available values |Description |
| -------- | -------------- | ----------- | ------ | ------ |
| Position | `data-position` | `'bottom'` | `bottom`, `top`, `left`, `right` | This controls which direction the popup will open relative to the button |
| Alignment | `data-alignment` | `'center'` | `start`, `center`, `end` | This controls the alignment of the popup will open relative to the button |
| Point | `data-point` | `'false'` | | This controls whether the popup has a point on it or not |
| Hover | `data-hover` | `'false'` | | This controls whether hovering the mouse over the button will open the popup |

| Events | Dispatches/Listens | Description |
| ------ | ------------------ | ----------- |
| `toggleButtonOn` | Dispatches | This event is dispatched when the button is toggled to the on/expanded state |
| `toggleButtonOff` | Dispatches | This event is dispatched when the button is toggled to the off/collapsed state |
| `toggleElementOn` | Dispatches | This event is dispatched when the element is toggled to the on/expanded state |
| `toggleElementOff` | Dispatches | This event is dispatched when the element is toggled to the off/collapsed state |
| `commandClose` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button off/collapsed |
| `commandOpen` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button on/expanded |
| `commandToggle` | Listens | The component will listen for this event on both the button and toggled element, when the event is heard it will try to toggle the button state |
| `popupOpen` | Dispatches | When the popup opens this event will dispatch, this is needed due to the extra logic involved with popups closing other popups |

| Keys | Actions |
| ---- | ------- |
| `space` | Toggles the state |
| `escape` | Tries to toggle off/collapsed |

_These keys only work when focus is on the button_

```html
<!-- Popup Example With Data Attributes -->
<div class="dcf-popup" data-position="top" data-alignment="center" data-point="true">
  <button class="dcf-btn dcf-btn-primary dcf-btn-toggle-popup">Open Popup Top and Center</button>
  <div class="dcf-popup-content unl-bg-cerulean dcf-rounded dcf-p-3">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean luctus hendrerit urna quis pellentesque. Aenean tempor est commodo nisi gravida interdum.
  </div>
</div>

<!-- Popup Example With Close Button -->
<div class="dcf-popup">
  <button class="dcf-btn dcf-btn-primary dcf-btn-toggle-popup">Open Popup With Close Button</button>
  <div class="dcf-popup-content unl-bg-cerulean dcf-rounded dcf-p-3">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean luctus hendrerit urna quis pellentesque. Aenean tempor est commodo nisi gravida interdum.
    <button class="dcf-btn dcf-btn-primary dcf-btn-close-popup">Close Popup</button>
  </div>
</div>

<!-- Popup Example With Hover-->
<div class="dcf-popup dcf-mt-6" data-hover="true">
  <button class="dcf-btn dcf-btn-primary dcf-btn-toggle-popup">Open Popup Hover</button>
  <div class="dcf-popup-content unl-bg-cerulean dcf-rounded dcf-p-3">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean luctus hendrerit urna quis pellentesque. Aenean tempor est commodo nisi gravida interdum.
    <button class="dcf-btn dcf-btn-primary dcf-btn-close-popup">Close Popup</button>
  </div>
</div>
```

# Scroll Animations
Pair the following JavaScript with [CSS classes](https://github.com/unl/wdntemplates/wiki/CSS#scroll-animations) to animate elements on page scroll.

```html
<script>
  window.addEventListener('DOMContentLoaded', function() {
    WDN.initializePlugin('scroll-animations');
  }, false);
</script>
```

# Search Selects

Search selects is a simplified term for multi-select combo boxes. This component is a wrapper around a normal select tag which makes it a little more user friendly and makes multi-selects actually nice to use. In the past we used select2 in place of this but that has limitations like bad UI/UX in dark mode. This component rely on specific CSS classes and does have CSS animations that will take place during the use.

The original select element should have the `hidden` attribute since a whole new set of elements will be appended after it. If the `hidden` attribute is not set then you will see two selects (the original and the `dcf-search-select`).

The user can type in the combobox to search for an item to select. Adding the `multiple` attribute to the original select will allow the user to select multiple items. The `disabled` and `readonly` attributes will be transferred over to the search select. If the page loads with options selected in the original select those will be transferred over to the search select.

Any selections in the search select will be synced with the search so no additional logic is needed when submitting the form, as long as the original select works then the search select should too.

```html
<form class="dcf-form">
  <div class="dcf-form-group">
    <label for="ice-cream-flavors">Ice Cream Flavors</label>
    <select id="ice-cream-flavors" name="ice_cream_flavors[]" multiple hidden class="dcf-search-select">
      <option value="Vanilla">Vanilla</option>
      <option value="Chocolate">Chocolate</option>
      <option value="Coffee">Coffee</option>
      <option value="Strawberry">Strawberry</option>
      <option value="Pistachio">Pistachio</option>
      <option value="Butter Pecan">Butter Pecan</option>
    </select>
  </div>
</form>

<!-- This is only required once per page with a search-select -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('search-selects');
  }, false);
</script>
```

# Tabs

Tabs are a standard UI design pattern. The implementation of this component has evolved over the years so there are many ways to define a tabs section in the HTML. This component rely on specific CSS classes.

Tabs can either be defined by using a `ul`/`ol` tag for the tab links, or we can add the class `dcf-tabs-panel-title` on an element to declare the text of the tab link. If we omit the `ul`/`ol` and do not define an element with `dcf-tabs-panel-title` then the tab link's text will be set as `Untitled`.

| Options  | Data Attribute | Default value | Description |
| -------- | -------------- | ----------- | ------ |
| Default Tab | `data-default` | `'false'` | This can be set to `true` on a tab panel and if it is set then when the page loads then that tab will be opened by default if no URL hash is found |
| Tab Hidden | `data-tab-hidden` | `'false'` | This can be set to `true` on a tab panel to hide that tab panel. We can also set the `hidden` attribute on the tab link to hide the tab if we define the `ol`/`ul` |
| URL Tracking | `data-url-tracking` | `'false'` | This can be set to `true` on the tab group and this will track the selected tab panel via a URL parameter instead of just the URL hash. This is helpful if your backend code needs to know which tab the user was on |

| Events | Dispatches/Listens | Description |
| ------ | ------------------ | ----------- |
| `ready` | Dispatches | When the specific tab group is finished being initialized this event will be dispatched |
| `tabSwitched` | Dispatches | When the specific tab group's selected tab is switched this event will be dispatched |
| `commandSwitch` | Listens | Each tab panel will listen for this event and when it is heard the tab group will switch to that panel |
| `commandPrev` | Listens | The tab group listens for this event and when it is heard the tab group will switch the tab to the previous tab (this does not wrap around to the last tab when we get to the beginning of the list) |
| `commandNext` | Listens | The tab group listens for this event and when it is heard the tab group will switch the tab to the next tab (this does not wrap around to the first tab when we get to the end of the list) |
| `commandHome` | Listens | The tab group listens for this event and when it is heard the tab group will switch the tab to the first tab |
| `commandEnd` | Listens | The tab group listens for this event and when it is heard the tab group will switch the tab to the last tab |

| Keys | Actions |
| ---- | ------- |
| `arrowLeft` | Switches to previous tab (this does not wrap around to the last tab when we get to the beginning of the list) |
| `arrowRight` | Switches to next tab (this does not wrap around to the first tab when we get to the end of the list) |
| `home` | Switches to the first tab |
| `end` | Switches to the last tab |

```html
<!-- Example Link to tab panel-->
<a href="#group3-panel2">Go To Tabs Panel #group3-panel2</a>

<!-- Tabs Example No UL -->
<div class="dcf-tabs" id="tabGroup3">
  <h3>Tab Group No UL</h3>
  <section id="group3-panel1">
    <h4 class="dcf-tabs-panel-title">Panel 1</h4>
    <p>...</p>
  </section>
  <section id="group3-panel2">
    <h4 class="dcf-tabs-panel-title">Panel 2</h4>
    <p>...</p>
  </section>
  <section id="group3-panel3" data-tab-hidden="true">
    <h4 class="dcf-tabs-panel-title">Panel 3</h4>
    <p>...</p>
  </section>
  <section id="group3-panel4">
    <h4>Panel 4</h4>
    <p>...</p>
  </section>
</div>

<!-- This is only required once per page with a tabs -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('tabs');
  }, false);
</script>
```

```html
<!-- Tabs Example Ordered List, Sections -->
<div class="dcf-tabs dcf-tabs-responsive" data-url-tracking="true">
  <h3>Tab Group (Ordered List, Sections)</h3>
  <ol>
    <li><a href="#group2-panel1" hidden>Tab 1</a></li>
    <li><a href="#group2-panel2">Tab 2</a></li>
    <li><a href="#group2-panel3">Tab 3</a></li>
  </ol>
  <section id="group2-panel1">
    <h4>Panel 1</h4>
    <p>...</p>
  </section>
  <section id="group2-panel2">
    <h4>Panel 2</h4>
    <p>..</p>
  </section>
  <section id="group2-panel3" data-default="true">
    <h4>Panel 3</h4>
    <p>...</p>
  </section>
</div>

<!-- This is only required once per page with a tabs -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('tabs');
  }, false);
</script>
```

```html
<!-- Tabs Example Unordered List, Divs -->
<div class="dcf-tabs dcf-tabs-responsive">
  <h3>Tab Group (Unordered List, Divs)</h3>
  <ul>
    <li><a href="#group1-panel1">Tab 1</a></li>
    <li><a href="#group1-panel2">Tab 2</a></li>
    <li><a href="#group1-panel3">Tab 3</a></li>
  </ul>
  <div id="group1-panel1">
    <h4>Panel 1</h4>
    <p>...</p>
  </div>
  <div id="group1-panel2">
    <h4>Panel 2</h4>
    <p>...</p>
  </div>
  <div id="group1-panel3">
    <h4>Panel 3</h4>
    <p>...</p>
  </div>
</div>

<!-- This is only required once per page with a tabs -->
<script>
  window.addEventListener('inlineJSReady', function() {
    WDN.initializePlugin('tabs');
  }, false);
</script>
```


# Using RequireJS and jQuery
The UNLedu framework uses a tool called [RequireJS](http://www.requirejs.org/) to load JavaScript libraries and dependencies. This guide will walk you through some RequireJS basics, including how to load JavaScript dependencies safely. At first glance, this might seem needlessly complex, but it is actually pretty simple. RequireJS has some great [documentation](http://www.requirejs.org/docs/api.html) on how to use it. We won’t dive into the details here, only the basics.

## Loading jQuery
Simply use the `require` function. The first parameter should be an array of dependencies, and the second parameter should be an anonymous function to run after the dependencies have loaded. The parameters for the anonymous function are mapped to the first parameter of the require function.

```javascript
require(['jquery'], function($) {
    //place any code that relies on $ here
});
```

## Loading Multiple and Custom Libraries
See the loading jQuery example for details on how the require function works

```javascript
require(['absolute path to library', 'jquery'], function(loadedLib, $) {
    //place any code that relies on $ and loadedLib here
});
```

## Configuring RequireJS
So now that you're convinced that RequireJS is awesome, let's cover how to configure it to work with your dependencies that are not a part of the framework. By default, we set the baseUrl configuration value to the base JavaScript directory for framework bundled dependencies. It should be no surprise that this won't work for module dependencies that you want to host in your own directory structure. To work around this, you should set a paths configuration value for each local dependency.

```javascript
require.config({
    paths: {
    "local-module-name": "url/to/local-module-name"
    }
});
```
If your website or project has a lot of javascript dependencies, it might be worth configuring RequireJS to search certain paths on your server for the correct JavaScript file. See the [RequireJS documentation](http://www.requirejs.org/docs/api.html#config) for details on how to accomplish this.

## Dealing with Dependencies That Are Not AMD Loader Friendly/Ready
While many JavaScript plugins and modules are adopting AMD loaders, there is a chance you will come across something that still uses the old way of relying on variables in the global scope. We’ve prepared a common jQuery dependency wrapper that can be put around these scripts so they work with the module loader.

**header:**
```javascript
(function(factory) {
    if (typeof define === 'function' && define.amd) {
    // AMD
    define(['jquery'], factory);
    } else if (typeof module === 'object' && module.exports) {
    factory(require('jquery'));
    } else {
    // Browser globals
    factory(jQuery);
    }
}(function(jQuery) {
```
**footer:**
```javascript
}));
```