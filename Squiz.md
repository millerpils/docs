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

Tag                                                         Function

%\_\_custom-contents%                                       prints standard editing area type
%metadata-F_metadata_values%                                prints all editing fields for metadata
%globals_asset_metadata_source%                             Retrieves metadata titled ‘source’
%form_errors%
%reset_button%
%submit_button%
%./?a=%asset_assetid%:v1                                    Retrieves first variety of an image
%./?a=%asset_assetid%:v2                                    Second variety
%asset_name_linked%                                         name of the asset linked to the asset
%asset_url%
%asset_thumbnail%                                           Retrieves thumbnail
%asset_contents%                                            Goes in paint layout
%paint_layout%                                              Goes in paint layout/page content
%asset_contents_paint_458661%                               Insert content from paint layout
%asset_metadata_dog1^replace_keywords:notempty:’{tags}’%    Test if metadata not empty
%asset_metadata_dog1^replace_keywords:empty:’{tags}’%       Test if empty
%list_current_asset_metadata_CUL.courses%                   ?

## Asset URLS

Sometimes global asset is required:

%begin_asset_url%
    <a href="%asset_url%">
%end_asset_url%

%begin_global_asset_url%
    <a href="%asset_url%">
%end_global_asset_url%