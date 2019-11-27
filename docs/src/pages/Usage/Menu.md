---
name: Customize menu
route: /menu
menu: Features
---

# Customize menu
Now you can order the menu and create new links from your config file like this:

// doczrc.js
export default {
  menu: [
    'Home',
    'Components',
    { name: 'Github', href: 'https://github.com/pedronauck/docz' },
  ],
}
And even reorder submenus:

// doczrc.js
export default {
  menu: [
    'Home',
    { name: 'Components', menu: ['Alert', 'Button'] },
    { name: 'Github', href: 'https://github.com/pedronauck/docz' },
  ],
}

Source: [Relase notes](https://github.com/doczjs/docz/releases/tag/v0.12.4)
