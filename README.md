# ga-wrapper
Google Analytics wrapper, automation via inline attributes and bindings.

Google Analytics wrapper (gaw) assumes use of the category, action, and label parameters, and that category is the top-level element in your event naming conventions.  

gaw will send an event when an element has all 3 parameters defined, whether explicitly from it's own attributes or implicitly from parent attributes.

# Setup  
```
//isogram code here
<script src="/javascript/gaWrapper.js"></script>  
<script>var gaw = new GAWrapper();</script>
```
  
# Options  
**prefix**  
String, prefixes category parameter  
  
**testMode**  
Boolean, disables push to analytics, disables link click navigation  
  
**verbose**  
Boolean, enables verbose logging

# Inline event parameters
gaw uses a global event listener and inline data attributes to determine if a push event is necessary. Given the following code, clicking on `li` would send an event with the `category` "Featured Models", the `action` "Clicked Product Category", and the `label` "Example Product".  
```
<div data-ga-category="Featured Models">
  <ul data-ga-action="Clicked Product Category">
    <li data-ga-label="Example Product">Example</li>
    <li data-ga-label="Example Product">Example</li>
  </ul>
</div>
```  
  
  
# Event parameter bindings
gaw supports bindings using the @ syntax. The following would replace @test with the clicked element's text.
  

```
<div data-ga-category="Featured Models">
  <ul data-ga-action="Clicked Product Category">
    <li data-ga-label="@element-text">Example 1</li>
    <li data-ga-label="@element-text">Example 2</li>
  </ul>
</div>
```
```
gaw.bind('element-text', function(element) {
    return $(element).text();
});
```  
  
  
# Dynamic event parameters  
gaw also supports dynamic parameters via ga-bind.

```
<div data-ga-category="Featured Models">
  <ul data-ga-action="Clicked Product Category" data-ga-bind-label="@element-text">
    <li data-ga-label>Example 1</li>
    <li data-ga-label>Example 2</li>
  </ul>
</div>
```
```
gaw.bind('element-text', function(element) {
    return $(element).text();
});
```  
  
  
# API  
***gaw.bind(keyword, fn)***  
registers a binding to replace based on the given function  
  
keyword, String, binding name  
  
fn, Function, logic to replace keyword with  
  
  
***gaw.push(category, action, label, element)***  
pushes an event to Google Analytics given non-empty params. Element is optional.  
  
  
category, String, the event category.  
  
action, String, the event action.  
  
label, String, the event label.  
  
element, Object, the element that triggered the push.  
  
# Dependencies
***jQuery***
