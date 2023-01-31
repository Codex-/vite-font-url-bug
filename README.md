# vite font url bug

This is a minimum reproduction repository for an issue where an invalid url is output during a vite build if you use a full url as the base.

This simply specifies a full URL as the base

```ts
export default defineConfig({
  ...
  base: "https://assets.site.com/",
});
```

Reference the font asset as you normally would:

```html
<style>
  @font-face {
    font-family: "Arial";
    src: local("Arial"), url("/fonts/Arial.ttf") format("truetype");
  }
</style>
```

Perform a build with `npm run build`

The parameter that is generated during a build for the `url()` call is invalid:

```html
<style>
  @font-face {
    font-family: "Arial";
    src: local("Arial"),
      url("https:/assets.site.com/fonts/Arial.ttf") format("truetype");
  }
</style>
```

The generated source has the incorrect amount of `/`s after `http:`
