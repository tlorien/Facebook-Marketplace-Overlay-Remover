#Facebook Marketplace Overlay Remover

This userscript is designed to allow access to Facebook Marketplace listings **without a Facebook account**. It does this by taking a heuristic approach to removing overlays and elements that block interaction with the page. The approach used should dynamically identify and eliminate intrusive elements without requiring updates whenever Facebook makes changes to its site.

## Installation
This userscript is hosted on [Greasy Fork](https://greasyfork.org/en/scripts/530181-facebook-marketplace-overlay-remover) and other popular userscript repositories. To install:

1. Install a userscript manager in your browser ([Violentmonkey](https://violentmonkey.github.io/get-it/) is recommended).
2. Visit [Greasy Fork - Facebook Marketplace Overlay Remover](https://greasyfork.org/en/scripts/530181-facebook-marketplace-overlay-remover) to find the latest version of the script.
3. Click on the "Install" button on the Greasy Fork page.

Once installed, the script will automatically run whenever you visit Facebook Marketplace. It operates in the background, removing any overlays that fit the heuristic criteria without any interaction needed from the user.

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
