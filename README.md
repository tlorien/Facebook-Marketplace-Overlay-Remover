# Facebook Marketplace Overlay Remover

This userscript allows access to Facebook Marketplace listings **without a Facebook account**! It does this by taking a heuristic approach to removing overlays and elements that block interaction with the page.

This approach should dynamically identify and eliminate intrusive elements without requiring updates whenever Facebook makes changes to its site.

![pic1](https://greasyfork.org/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTcxNTk1LCJwdXIiOiJibG9iX2lkIn19--bda2b45f9bc7e4f0912ae324b94cda51cb029650/pic2%20(2).png?locale=en "")
![pic2](URLhttps://greasyfork.org/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MTcxNTk2LCJwdXIiOiJibG9iX2lkIn19--16a399716c7826e267f077da1bd043e1f2ef7190/pic3%20(2).png?locale=en "")

## Installation
This userscript is hosted on [Greasy Fork](https://greasyfork.org/en/scripts/530191-facebook-marketplace-overlay-remover) and other popular userscript repositories. To install:

1. Install a userscript manager in your browser ([Violentmonkey](https://violentmonkey.github.io/get-it/) is recommended).
2. Visit [Greasy Fork - Facebook Marketplace Overlay Remover](https://greasyfork.org/en/scripts/530191-facebook-marketplace-overlay-remover) to find the latest version of the script.
3. Click on the "Install" button on the Greasy Fork page.

Once installed, the script will automatically run whenever you visit Facebook Marketplace. It operates in the background, removing any overlays that fit the heuristic criteria without any interaction needed from the user.

## The Script

```javascript
(function() {
    'use strict';
 
    function isLikelyOverlay(element) {
        const rect = element.getBoundingClientRect();
        const viewportArea = window.innerWidth * window.innerHeight;
        const elementArea = rect.width * rect.height;
        const coversMostOfTheViewport = elementArea > viewportArea * 0.5; // covers more than 50% of the viewport
        const isFixedOrAbsolute = ['fixed', 'absolute'].includes(getComputedStyle(element).position);
        const hasHighZIndex = parseInt(getComputedStyle(element).zIndex, 10) > 100;
 
        return coversMostOfTheViewport && isFixedOrAbsolute && hasHighZIndex;
    }
 
    function removeSuspectedOverlays() {
        document.querySelectorAll('body *').forEach(element => {
            if (isLikelyOverlay(element)) {
                element.remove();
            }
        });
    }
 
    removeSuspectedOverlays();
 
    const observer = new MutationObserver(mutations => {
        mutations.forEach(mutation => {
            if (mutation.addedNodes.length) {
                removeSuspectedOverlays();
            }
        });
    });
 
    observer.observe(document.body, {
        childList: true,
        subtree: true
    });
 
})();
```

## How It Works
The script examines each element in the document body to determine if it behaves like an overlay based on several criteria:

**Coverage**: The element covers more than 50% of the viewport.
**Positioning**: The element is fixed or absolute.
**Visibility**: The element has a high z-index.

These properties typically characterize the overlays designed to block user interaction and do not appea to affect the other required elements.

## Contributing
If you have suggestions, bug reports, or enhancements, please feel free to open an issue or submit a pull request.

## License
This script is distributed under the MIT License. See the LICENSE file for more details.
