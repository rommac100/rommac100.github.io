---
layout: post
title:  "Firefox Customization"
date:   2020-09-07 
tags: [software]
permalink: /firefox-custom
---

## Summary
 This page will contain the various tweaks I have made to firefox. I will try to keep the ones that I actively use updated (though know guarantees).

## User Chrome
If you have not looked into userChrome customization on firefox checkout the [sub reddit](https://www.reddit.com/r/FirefoxCSS/) that specializes it.
Specifically, this [post](https://www.reddit.com/r/FirefoxCSS/comments/73dvty/tutorial_how_to_create_and_livedebug_userchromecss/) gives some useful links and info on how to setup userChrome.

# Hide Url Bar + tab bar (2020-09-07)
```css
#TabsToolbar { visibility: collapse }

#titlebar { visibility: collapse; }

#PersonalToolbar{ --uc-bm-height: 20px; --uc-bm-padding: 4px; --uc-autohide-toolbar-delay: 200s; --uc-autohide-toolbar-focus-rotation: 0deg; --uc-autohide-toolbar-hover-rotation: 0deg; }

:root[uidensity="compact"] #PersonalToolbar{ --uc-bm-padding: 1px }
:root[uidensity="touch"] #PersonalToolbar{ --uc-bm-padding: 7px }

#PersonalToolbar:not([customizing]){ position: relative; margin-bottom: calc(0px - var(--uc-bm-height) - 2 * var(--uc-bm-padding)); transform: rotateX(90deg); transform-origin: top; z-index: 1; }

#PlacesToolbarItems > .bookmark-item{ padding-block: var(--uc-bm-padding) !important; }

#nav-bar:focus-within + #PersonalToolbar{ margin-top: 61px; margin-bottom: -61px; transform: rotateX(var(--uc-autohide-toolbar-focus-rotation,0)); }

#navigator-toolbox:hover > #PersonalToolbar{ margin-top: 61px; margin-bottom: -61px; transform: rotateX(var(--uc-autohide-toolbar-hover-rotation,0)); }

#navigator-toolbox:hover > #nav-bar:focus-within + #PersonalToolbar {  margin-top: 61px; margin-bottom: -61px; transform: rotateX(0); }

#nav-bar:not([customizing="true"]):not([inFullscreen]) { min-height: 0px !important; max-height: 0px !important; margin-top: 8px !important; margin-bottom: -1px !important; z-index: -5 !important; }

#navigator-toolbox:hover:not([inFullscreen]) :-moz-any(#nav-bar), 
#navigator-toolbox:focus-within :-moz-any(#nav-bar) {
min-height: 32px !important; max-height: 32px !important; margin-top: 8px !important; margin-bottom: -61px !important; z-index: 5 !important; }

#urlbar { --urlbar-toolbar-height: 32px !important; }
```

## DNS over HTTPS:
 - So this a relatively new [circa 2020](https://blog.mozilla.org/en/products/firefox/firefox-continues-push-to-bring-dns-over-https-by-default-for-us-users/) roll out that I was not aware of and causes issues with local dns without proper certificates. The solution is to just disable the DNS over HTTPS option in your Network Settings of firefox. *Note have not thoroughly checked the problems that are associated performing this check*
<img src="/_images/electronics/riscv/pwmmem.png" width="75%" height="75%"/>

## Plugins
 - [Ghostery](http://www.ghostery.com/) - nice for removing trackers and some ads
 - [Last Pass](https://lastpass.com/) - good enough password manager
 - [Tree Style Tabs](http://piro.sakura.ne.jp/xul/_treestyletab.html.en) - basically my solution to being able to see my tabs using a shortcut (though now on vertical instead of horizontal tabs which is fine imo)
 - [uBlock Origin](https://github.com/gorhill/uBlock#ublock-origin) - By far the best adblock atm. Lots of customization available.

