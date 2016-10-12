# Advanced Theme Builder
Advanced theme builder is a modular content creator for Shopify themes.   


## Installation

### Automatic
1. Download install the Advanced Theme Builder app from the Shopify app store.

### Manual
1. Copy the atb.liquid and atb-render.liquid into your Shopify theme snippets folder.
2. Upload the files or use the Shopify file editor and save.


## Add Zones to Theme Files
Once you have the atb.liquid and atb-render.liquid files installed in your theme, you may begin adding zones to your theme template files. Page, article, product, and collection templates are eligible for zones.   
1.  Choose a template file.  (eg. product.liquid)
2.  Insert the following code where you would like your zone. `{% include 'atb' zone:"First-Area"%}` Each zone is given a name such as 'First-Area'.   Zone names must consist of only letters, numbers, and dashes.


