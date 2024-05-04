---
tags:
  - web
  - css
---
Displaying a local/remote web font with CSS

```css
/* load preferred font */
@font-face {
  font-family: 'Berkeley Mono';
  font-style: normal;
  font-weight: 400;
  font-display: fallback;
  src: local('Berkeley Mono'),
    url('https://cdn.runtimeterror.dev/fonts/BerkeleyMono.woff2') format('woff2'),
}
```

More @[runtimeterror](https://runtimeterror.dev/using-custom-font-hugo/)