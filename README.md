# *Hyperfast* Static Websites
This repo is the basis for a small tool I'm trying to build. I don't know what technology is most suitable yet or how best to achieve some of these aims, so I'm opening this up to group discussion. 

## Aim
A way to create static sites that are served in literally the fastest way possible. Time-to-first-byte, first rendering on screen, everything optimised to be utterly, stupidly, quick. Use react or similar to make navigation around the site instant, but provide a raw HTML+CSS fallback for search engines and users without JS. 

## Specfic features 
Let's start with a simple blog or marketing site that uses react<sup>1</sup> to instantly switch between pages. Pages are react components. 
<sup>1</sup> I don't really care which library is used. When switching between pages most of the DOM is getting re-rendered anyway, so maybe this is overkill. Maybe just replace the body to avoid those React KB. 
```
+ Site navigation is instant
- Non-js users can't see anything
- All JS & CSS must load before the user sees anything. This takes anything from 150ms to 20s (slow connection). 
``` 

That 150-1000+ms delay while assets are downloaded, parsed & rendered is unnaceptable here. Non-js users are also screwed. 
So let's generate HTML (serverside or by our tool on deploy) and serve that first. Our JS then loads in the background and replaces the page with our React app. 
```
+ Site navigation is instant
+ Non-js users see the site, they can navigate between HTML pages like normal (non-instant, but that's expected). 
+ Intitial page load is much faster because the HTML is sent right away. 
- CSS for the whole site must be downloaded and parsed before rendering.
- HTML for the whole page must be downlaoded and parsed before rendering.
```

*Almost* there. This is a really cool idea that [a few](https://github.com/jxnblk/react-static-site-boilerplate) [people](https://github.com/koistya/react-static-boilerplate) have already been working on. 
Two issues remain. Firstly, we can still make the pages load faster. We're making the page block while it waits for the whole site's CSS, so let's inline a few select styles and then load the CSS async. 
Secondly, I'm not convinved React is needed here at all. Technically it's probably the fastest way to render the page transitions, but at the cost of adding ~100kb of extra JS. 

Proposal: What if we were to load a fragment of HTML + CSS, served inline, before loading the rest of the site asyncrhonously and then fading it in? 

TBC... 
