# Advanced Theme Builder
Advanced theme builder is a modular content builder for Shopify themes.  It takes JSON data stored in Shopify metafields and renders HTML content based on section templates.  After installing the [Advanced Theme Builder](https://apps.shopify.com/) Shopify app, go to the [Advanced Theme Builder section store](http://apps.sltwtr.com/advancedthemebuilder/store/) to upload sections directly into your Shopify store.


## Installation

### Automatic
1. Download install the Advanced Theme Builder app from the Shopify app store.

### Manual
1. Copy the atb.liquid and atb-render.liquid into your Shopify theme snippets folder.
2. Upload the files or use the Shopify file editor and save.


## Add Zones to Theme Files
Once you have the atb.liquid and atb-render.liquid files installed in your theme, you may begin adding zones to your theme template files. Page, article, product, and collection templates are eligible for zones.   

1.  Choose a template file.  (eg. product.liquid)
2.  Each zone is given a name such as *First-Area*.   Zone names may contain only letters, numbers, and dashes.
3.  Insert the following code in your template file where you would like your custom content: `{% include 'atb' zone:"First-Area"%}` 


## Create Your Own Section Templates

### Schema

Each section template contains a schema. 

1. Schemas define section details such as name, descrtipion, tags, and icon.
2. The schema id must match the file name - atb.{id}.liquid
3. Required schema attributes are:
  + **name** - the name of your section 
  + **id** - unique id of your section - must match file name
  + **banner** - banner image used in the section store
  + **icon** - the icon to be displayed in advanced theme builder
  + **tags** - tags are used for searching the section store
  + **description** - a helpful description of your app and included in app store search
  + **settings** - an array of variables used by your section
4. Setting attributes are:
  + **type** - the input type for the form input
    - text
    - textarea
    - html
    - select
    - colorpicker
    - image
    - product
    - page
    - collection
  + **id** - this will be the variable name
  + **label** - input item label
  + **info** - input item description
  + **default** - default value 
  + **repeatable** - true or false, value becomes an array
  + **options** - select options (only for type select)

5. Here is a sample schema:
```json
{
  "name": "Repeater Demo",
  "id": "repeater-demo",
  "banner": "https://s3.amazonaws.com/shopify-app-store/shopify_applications/small_banners/6152/splash.png?1460647934",
  "icon": "https://apps.sltwtr.com/advancedthemebuilder/atb/ui/offset.png",
  "tags": "jquery, offset2, bootstrap",
  "decsription": "this is the awesome offset block",
  "settings": [
    {
      "type": "text",
      "id": "title",
      "label": "Title",
      "info": "The title goes here",
      "default": "Titlest"
    },
    {
      "type": "select",
      "id": "size",
      "label": "Size",
      "info": "How big?",
      "default": "large",
      "options": [
        {
          "value": "xx-small",
          "label": "XX Small"
        },
        {
          "value": "x-small",
          "label": "X Small"
        },
        {
          "value": "small",
          "label": "Small"
        },
        {
          "value": "medium",
          "label": "Medium"
        },
        {
          "value": "large",
          "label": "Large"
        },
        {
          "value": "x-large",
          "label": "X Large"
        },
        {
          "value": "xx-large",
          "label": "XX Large"
        }
      ]
    },
    {
      "type": "colorpicker",
      "id": "color",
      "label": "Color",
      "default": "#FF0000",
      "info": "This is the color"
    },
    {
      "type": "image",
      "id": "my_image",
      "label": "Image",
      "default": "",
      "info": "Pick the best image"
    },
    {
      "type": "product",
      "id": "product1",
      "label": "Product",
      "default": "",
      "info": "Pick a product",
      "repeatable": true
    },
    {
      "type": "page",
      "id": "page1",
      "label": "Page",
      "default": "",
      "info": "Pick a page"
    },
    {
      "type": "collection",
      "id": "collection1",
      "label": "Collection",
      "default": "",
      "info": "Pick a collection"
    },
    {
      "type": "textarea",
      "id": "summary",
      "label": "Summary",
      "default": "Sum it up",
      "info": "Summarize it"
    },
    {
      "type": "html",
      "id": "description",
      "label": "Description",
      "info": "You can add html here"
    }
  ]
}
```

## Rendering Variables

1.  Add the following code above your html `{% include 'atb-render' field:'my_image' %}` where my_image is the id of an option.
2.  In the next line, add `{% assign my_image = val %}`.  The previous line assigned our value to a variable called val.  Now we assign it val to a new variable with a proper descriptive name.
3.  If the setting is *repeatable*, **val** will be an *array*.
4.  Product, collection, and page types return the handle or slug.   To obtain the entire product object from its handle, use all_products[handle].

