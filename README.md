# NEAR Global Footer

Provides a CDN-powered endpoint to access the HTML and CSS for the near.org footer for use throughout the ecosystem.

## Access

We use [Statically](https://statically.io/) to access these files and provide CDN functionality.

To access the latest from `main`:

- `https://cdn.statically.io/gh/nearprotocol/near-global-footer/main/footer.txt`
- `https://cdn.statically.io/gh/nearprotocol/near-global-footer/main/footer.css`

To access from a specific commit hash, say `acdefee`:

- `https://cdn.statically.io/gh/nearprotocol/near-global-footer/acdefee/footer.txt`
- `https://cdn.statically.io/gh/nearprotocol/near-global-footer/acdefee/footer.css`

## Caching

Statically caches all files 1 year, except for these branches that are cached for only 1 day:

- `main`
- `master`
- `dev`
- `develop`
- `gh-pages`

In general, reference the `main` branch and you'll get the updated code within 1 day at the longest.

## Icons

The social icons are powered by Font Awesome. If you have Font Awesome included on your property already, you probably won't need to do anything. Otherwise, you can include this JavaScript file:

```html
<script src="https://use.fontawesome.com/releases/v5.15.4/js/brands.js"></script>
```

## Implementation

Implementation is up to you and will depend largely on your environment. Here are a couple of working examples to get you started though.

### Static HTML/CSS

```html
<link rel="https://cdn.statically.io/gh/nearprotocol/near-global-footer/main/footer.css">

<div id="global-footer"></div>

<script>
    fetch('https://cdn.statically.io/gh/nearprotocol/near-global-footer/main/footer.txt')
        .then(res => res.text())
        .then(html => {
            document.getElementById('global-footer').innerHTML = html
        })
</script>
```

### React

This is useful for Docusaurus sites.

```js
import React, { useState, useEffect } from 'react'

function Footer() {
  const [error, setError] = useState(null)
  const [markup, setMarkup] = useState([])

  useEffect(() => {
    fetch('https://cdn.statically.io/gh/nearprotocol/near-global-footer/main/footer.txt')
      .then(res => res.text())
      .then(
        html => {
          setMarkup(html)
        },
        error => {
          setError(error)
        }
      )
  }, [])

  if (error) {
    return null
  } else {
    return (
      <div>
        <div dangerouslySetInnerHTML={{ __html: markup }} />
      </div>
    )
  }
}

export default Footer
```
