# Advanced Theme Builder
Advanced theme builder is a modular content builder for Shopify themes.  It takes JSON data stored in Shopify metafields and renders HTML content based on section templates.  After installing the [Advanced Theme Builder](https://apps.shopify.com/) Shopify app, go to the [Advanced Theme Builder section store](http://apps.sltwtr.com/advancedthemebuilder/store/) to upload sections directly into your Shopify store.

## Native Shopify Section Conversion
To convert Shopify sections into Advanced Theme Builder section, use our conversion tool (https://advancedthemebuilder.com/conversion/)

## Installation

### Automatic
1. [Download](https://apps.shopify.com/) install the Advanced Theme Builder app from the Shopify app store.

### Manual
1. Copy the atb.liquid and atb-render.liquid into your Shopify theme snippets folder.
2. Upload the files or use the Shopify file editor and save.


## Add Zones to Theme Files
Once you have the atb.liquid and atb-render.liquid files installed in your theme, begin adding zones to your theme templates. Page, article, product, and collection templates are all eligible for zones.   

1.  Choose a template file.  (eg. product.liquid)
2.  Select a name for your zone such as *First-Area*.   Zone names may contain only letters, numbers, and dashes.
3.  Insert the following code in your template file where you would like your zone: `{% include 'atb' zone:"First-Area"%}` 


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
{% comment %}
ATB-SCHEMA{
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
}ATB-SCHEMA
{% endcomment %}
```

## Rendering Variables

1.  Add the following code above your html `{% include 'atb-render' field:'my_image' %}` where my_image is the id of an option.
2.  In the next line, add `{% assign my_image = val %}`.  The previous line assigned our value to a variable called val.  Now we assign it val to a new variable with a proper descriptive name.
3.  If the setting is *repeatable*, **val** will be an *array*.
4.  Product, collection, and page types return the handle or slug.   To obtain the entire product object from its handle, use all_products[handle].

## Example
Here is a simple example Advanced Theme Builder section that adds a styled dividing line - atb.divider.liquid :

```
{% comment %}
ATB-SCHEMA{
	"name":"Dividing Line",
	"id":"divider",
	"price": 0,
	"banner":"//i.imgur.com/OcChZrR.png",
	"icon": "//i.imgur.com/ba3VsGM.png",
	"screenshots" : [
		"//i.imgur.com/OcChZrR.png",
		"//i.imgur.com/OcChZrR.png",
		"//i.imgur.com/OcChZrR.png"
	],
	"video" : "//player.vimeo.com/video/180350618",
	"tags": "divider,hr,universal,html",
	"description": "Separate your content with a dividing line.",
	"long_description": "Separate your content with a dividing line. Separate your content with a dividing line. Separate your content with a dividing line. Separate your content with a dividing line. Separate your content with a dividing line. Separate your content with a dividing line. Separate your content with a dividing line. Separate your content with a dividing line.",
	"settings":[
		{ 
			"id" : "color",
			"label" : "Line Color",
			"default" : "#000000",
			"info" : "Select a color for the dividing line",
			"type" : "colorpicker"
		},
		{ 
			"id" : "thickness",
			"label" : "Line Thickness",
			"info" : "Define line thickness",
			"default" : "1px",
			"options": [
				{
					"label": "1pt",
					"value": "1px"
				},
				{
					"label": "2pt",
					"value": "2px"
				},
				{
					"label": "3pt",
					"value": "3px"
				},
				{
					"label": "4pt",
					"value": "4px"
				},
				{
					"label": "5pt",
					"value": "5px"
				},
				{
					"label": "10pt",
					"value": "10px"
				}
			],
			"type" : "select"
		},
		{ 
			"id" : "width",
			"label" : "Divider Width",
			"default" : "90%",
			"info" : "Select a width for the dividing line",
			"type" : "select",
			"options": [
				{
					"label": "25%",
					"value": "25%"
				},
				{
					"label": "50%",
					"value": "50%"
				},
				{
					"label": "75%",
					"value": "75%"
				},
				{
					"label": "90%",
					"value": "90%"
				},
				{
					"label": "100%",
					"value": "100%"
				}
			]
		}
	]
}ATB-SCHEMA
{% endcomment %}

{% include 'atb-render' field:'color' %}
{% assign color = val %}

{% include 'atb-render' field:'thickness' %}
{% assign thickness = val %}

{% include 'atb-render' field:'width' %}
{% assign width = val %}

<hr style="border-bottom:{{color}} {{thickness}} solid; height:0px;border-top:none;width:{{width}}; margin-left:auto;margin-right:auto;"/>

```

### Repeaters

Any fields can be included in repeating groups by adding a repeatable repeatable property to the field and giving it a name.

```
repeatable: 'groupname'
```
