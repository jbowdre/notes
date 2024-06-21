---
tags:
  - web
  - javascript
  - api
---
### Sending

To send an event named `upvote {{ post_title }}` when the element with class `upvote-button` is clicked:

```html
<script>
  window.onload = function() {
    var button = document.querySelector('.upvote-button');
    if (button) {
      button.addEventListener('click', function(event) {
        cabin.event("upvote {{ post_title }}");
      });
    }
  };
</script>
```
([ref](https://docs.withcabin.com/events.html))

More @[weblog](https://blog.jbowdre.lol/tracking-bear-upvotes-from-my-cabin/)

### Retrieving (WIP)

I ultimately want to also display the count of events alongside the button (specifically on non-Bear sites). So far I've got this command to retrieve events from the public dashboard for a property:

```shell
curl -s 'https://withcabin.com/api/stats-public?domain=blog.jbowdre.lol&id=M0NgWW4YpQpk&startKey=2024-06-15&endKey=2024-06-21&dataType=PATH' | jq '.events[].children[] | {label, value}'                   
```
