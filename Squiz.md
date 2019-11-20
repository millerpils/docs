# Squiz

Squiz admin: https://www.city.ac.uk/_admin/
UN: ucswebteam

Staging: https://www.city.ac.uk/staging/labs/daniel-m

## FAQ

Q: nesting a template and the template doesn’t show up?

A: Add in the nested content container but keep blank, commit and then configure the template to use

## Testing

For testing purposes:

I have to clone a page where the content item resides and prefix with “dev whatever”

Clone the asset where the item is and prefix with “dev whatever”.

Create customisations somewhere?

Then point something to the dev version I cloned?

## Start Now CSS

Some CSS is generated using loops and mixins, so run searches to find vars, colours etc. Some forms a powered by react-forms, JS which generates the form. This is in a repo of its own.

## CityR Static CSS Version

Each theme has a static version that needs to be incremented by one once changes are made, for CityR, find it in file:

static-version (Id: #77379)

## Clear Cache

https://www.city.ac.uk/postgraduate-applicants
Header (for CityR and maybe CASS)

Right click a page, click settings then find the design attached
Content Container Template

To create this, right click your folder and go to New Child/Layouts/Content Container Template

## Edit+ Screen

https://www.cass.city.ac.uk/staging/labs/daniel/image-listing/_edit

## Paint Layouts

Like a container for the content and are applied to pages. Look under Type Formats for the contents with container tags etc. Dynamic content is then outputted using “keyword replacements” (tags)

## Metadata

Holds data which is used for templates. Helps make the content dynamic. Can have data like text, select, dropdown, time, HTML code.

Example Code

<div class="wrapper">
    <img alt="%asset_metadata_dog3^as_asset:asset_attribute_alt%" src="%asset_metadata_dog3^as_asset:asset_url%">
    <img src="./?a=453208">
    <img src="./?a=453207">
</div>

## Conditional Output

Can be set under page/conditions. Applied to the paint layout - the one below is for an if true/false test:

Right click default format under paint layouts/type formats and select conditional keywords

Using empty/not empty conditions:

%asset_metadata_dog1^replace_keywords:notempty:'
<img alt="{asset_metadata_dog1^as_asset:asset_attribute_alt}" src="{asset_metadata_dog1^as_asset:asset_url}">
'%

%asset_metadata_dog1^replace_keywords:empty:'
<img alt="{asset_metadata_dog1^as_asset:asset_attribute_alt}" src="{asset_metadata_dog1^as_asset:asset_url}">
'%

For a truthy test, just use begin/end with no prior condition set-up needed:

%begin_asset_metadata_card.record^as_asset:asset_metadata_person.profile.image%
%asset_contents_paint_450995^with_get:imageasset={asset_metadata_card.record^as_asset:asset_metadata_person.profile.image}%
%end_asset_metadata_card.record^as_asset:asset_metadata_person.profile.image%

## Adding Select Boxes

These are added via metadata fields. A default option can be selected then outputted as a style (for example):

style="border: 1px solid {asset_metadata_set.styles_value}"

## Images

Add an image in raw HTML: <img src="./?a=453209">

## Tags/Code

Tag Function

%\_\_custom-contents% prints standard editing area type
%metadata-F_metadata_values% prints all editing fields for metadata
%globals_asset_metadata_source% Retrieves metadata titled ‘source’
%form_errors%
%reset_button%
%submit_button%
%./?a=%asset_assetid%:v1 Retrieves first variety of an image
%./?a=%asset_assetid%:v2 Second variety
%asset_name_linked% name of the asset linked to the asset
%asset_url%
%asset_thumbnail% Retrieves thumbnail
%asset_contents% Goes in paint layout
%paint_layout% Goes in paint layout/page content
%asset_contents_paint_458661% Insert content from paint layout
%asset_metadata_dog1^replace_keywords:notempty:’{tags}’% Test if metadata not empty
%asset_metadata_dog1^replace_keywords:empty:’{tags}’% Test if empty
%list_current_asset_metadata_CUL.courses% ?

## Asset URLS

Sometimes global asset is required:

%begin_asset_url%
<a href="%asset_url%">
%end_asset_url%

%begin_global_asset_url%
<a href="%asset_url%">
%end_global_asset_url%

## As_asset

You can get info from an asset by tacking this on to a keyword replace, eg

```html
<a href="%asset_metadata_person.organisation.department^as_asset:asset_url%">
  %asset_metadata_person.organisation.department^as_asset:asset_name%
</a>
```

### As asset tags

^as_asset:asset_contents_raw

## Include paint layout by ID

%globals_asset_contents_paint_layout_id_474151%

## Include contents of asset with get

%globals_asset_contents_raw:460079^with_get:assets={493718}%

## Conditions

If/else

```javascript
    %begin_asset_metadata_xcri.course.title%
        %asset_metadata_xcri.course.title%
    %else_asset%
        %asset_metadata_DC.title%
    %end_asset%
```

Equal to

%begin_asset_metadata_non.academic.profile.type^eq:alumni%
// code
%end_asset%

## Getting metadata from referenced related assets

```
%frontend_asset_metadata_course.courses.parentcourse^as_asset:asset_metadata_course.courses.bundle.price%
```

Above parentcourse is a related asset, which we're accessing the bundle price field from.

## Asset listings

Variable names and values can be passed from the page asset (or other asset such as the PL that's
rendering the asset) into the asset listing. This then restricts the results and returns the values specified
in the asset listing configuration.

EG:

Page asset ->
Nested asset listing
Var name: parentid
Var value: %frontend_asset_metadata_course.courses.parentcourse%

Asset listing ->
Replacement Root node for the listing (must be a child of the static root node)
parentid

We can then print what we need to print in page contents/default format.

NB: if using GET vars, remember to select GET Variable Name from the dropdown and
not Set Value

##

## Serverside JS examples

### Get metadata and display as links

```javascript
    <script runat="server">
        var centres = %asset_metadata_organisation.centre%;
        for (var i = 0; i < centres.length; i++) {
            print('<a href="%globals_asset_url:' + centres[i] + '%">%globals_asset_name:' + centres[i] + '%</a>');
            if ( centres.length > 1 && i !== centres.length - 1) {
                print(', ');
            }
        }
    </script>
```

### Nest cards

```javascript
    <script runat="server" evalkeywords="post">
    var asset = '%frontend_asset_metadata_subjects.pathway.cards%';
    print('%globals_asset_contents_raw:474907^with_get:assetid=' + asset + '%');
    </script>
```

### Print a paint layout with an asset

```javascript
    <script runat="server" evalkeywords="post">
    var asset = '493648'; print('%globals_asset_contents_paint_layout_id_450951:'
    + asset + '^with_get:pathway=pathway%');
    </script>
```

### Print asset metadata belonging to related assets

```javascript
    <script runat="server">
        var assets = %asset_metadata_modal.assets%;
        
        for (var i = 0; i < assets.length; i++) {
            print('<a href="%globals_asset_metadata_startdate.asset^asset_url:' + assets[i] + '%">%globals_asset_metadata_startdate.date-text:' + assets[i] + '% <span class="fas fa-calendar"></span></a>');
        }
    </script>
```

## Content container layouts

See #493801 for example

To list metadata on an SEL: %metadata-F_500751%

## Documentation

### Full width

See https://web2020.city.ac.uk/documentation/patterns/key-information-box.

Apply paint layout 478438
Apply metadata schema 478404
This gives you a field to pass in a related asset which will display full-width