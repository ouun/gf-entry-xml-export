# Gravity Forms Entry XML Export #
**Contributors:** thewebist  
**Tags:** gravityforms, xml  
**Requires at least:** 3.7  
**Tested up to:** 4.7.4  
**Stable tag:** 1.2.1  
**License:** GPLv2 or later  
**License URI:** http://www.gnu.org/licenses/gpl-2.0.html  

Writes out Gravity Forms submissions as XML files.

## Description ##

This plugin saves out all your Gravity Forms entries as XML files.

Should you want to rename the XML tags generated by your form, you can use the filter `gf_to_xml_array_keys` which supplies a form submission mapped to an array along with the form ID. Example:

```
function new_keys( $new_keys, $form_id )
{
    switch( $form_id )
    {
        default:
            $new_keys['First'] = 'first_name';
            $new_keys['Last'] = 'last_name';
        break;
    }
    
    return $new_keys;
}
add_filter( 'gf_to_xml_array_keys', 'new_keys', 10, 2 );
```

## Specifying where export files get saved ##

By default, entry XML files get saved in `wp-content/uploads/xml/`. You can also configure your forms to save XML files in a sub-directory inside `wp-content/uploads/xml/`. This can be achieved via either a user's selection for a drop down/radio field, or via a hidden field.

**Save the export in a user selected sub-directory:**

To save a form's export in a sub-directory based on a user's selection, do the following:

1. Create a user selectable field, and add options to the field with values that will be used for your sub-directory names.
2. Under the "Appearance" tab for the field, add a *Custom CSS Class* called `createdirectory`.

Now, when a user submits the form, his/her submission XML will be exported into a sub-directory of `wp-content/uploads/xml/`. That sub-directory will be named after the submitted value for the field with the `createdirectory`.

**Save the export via a hidden field specified sub-directory:**

To save a form's export in a sub-directory defined by a hidden field value, do this:

1. Create a hidden field.
2. Name the field `createdirectory`.
3. Set the value of the field to your preferred sub-directory name.

## Installation ##

1. Upload the plugin to the `/wp-content/plugins/` directory
2. Activate the plugin through the 'Plugins' menu in WordPress

## FAQs ##

### How do I start the XML export of my entries? ###

My code is hooked to `gform_after_submission`, so the plugin writes out the XML after a form is submitted. So, it doesn’t export existing entries, just new entries when they’re submitted.

### Where do entries get exported? ###

Entry XML files get exported here: `wp-content/uploads/xml/`. Additionally, you may specify sub-directories where a form's entries are saved. This means you can have a form save entries in different sub-directories based on user-selected form values or by values present in hidden fields. See the section *Specifying where export files get saved* for more details.

## Changelog ##

### 1.2.1 ###
* Skipping empty values when building form $data array for writing to XML. This should fix form exports from having empty values for required fields (e.g. empty telephone numbers).

### 1.2.0 ###
* Set the export sub-directory via a hidden field with the label of `createdirectory` and the value will be the name of the sub-directory.

### 1.1.0 ###
* Setting a Gravity Forms field's "Admin Field Label" specifies the name of the XML tag used to hold the field's data in the XML export
* Added special processing for a field's CSS classes. Currently there's only one optional class: `createdirectory` will use the value of the field to create a directory where the form's XML will be saved.

### 1.0.4 ###
* Updating `$lead_source` variable to be `SITE_URL - PAGE_TITLE`

### 1.0.3 ###
* Adding additional normalization for conversion of GF form field names to valid XML element names
* BUGFIX: Adding missing semicolon

### 1.0.2 ###
* Adding `page_title` to lead source

### 1.0.1 ###
* Adding sitename to XML export filename
* Changing date value to ISO 8601 date
* Removing illegal characters from XML tag names

### 1.0.0 ###
* Initial release
