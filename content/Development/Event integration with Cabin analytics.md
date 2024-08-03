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
        cabin.event("kudos");
      });
    }
  };
</script>
```
([ref](https://docs.withcabin.com/events.html))

More @[srs bsns (lol)](https://srsbsns.lol/tracking-bear-upvotes-from-my-cabin/)
