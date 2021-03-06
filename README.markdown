This is a plugin for [Hobo](http://hobocentral.net).
This is a direct port of paperclip_with_hobo plugin to a GEM.

This plugin wraps [paperclip](http://rubygems.org/gems/paperclip) for Hobo.

It adds two small things:

 - Automatically declares the fields for you, so you can just add
 
        has_attached_file :photo

   to your model, and then run the migration generator.   All options
   are automatically passed on to paperclip's `has_attached_file`.
   
 - Declares an input field
 
        <def tag="input" for="Paperclip::Attachment">
          <%= file_field_tag param_name_for_this, attributes %>
        </def>
        
   (to get this, you need `<include gem='hobo_paperclip'/>` in front_site.dryml)


### Installation

Paperclip is required so add it to your gemfile if you don't have it already

    gem 'paperclip'
    
Add hobo_paperclip to your gemfile (make sure you add it *below* paperclip, or it will fail with `undefined method 'has_attached_file' for module Paperclip::ClassMethods' (NameError)`):

	gem 'hobo_paperclip', :git => "git://github.com/Hobo/hobo_paperclip.git", :branch => "master"
	
Update your bundle:

    bundle install

Include the hobo_paperclip taglib in front_site.dryml
	
	<include gem='hobo_paperclip'/>

Add paperclip to one of your models:

    has_attached_file :photo

Your default form for the model will now include the four attributes
added by `has_attached_file`.  To actually allow uploading, you will
need to manually add the attachment field (`photo` in the above example)
to your form, and don't forget to add the `multipart` attribute:

    <extend tag="form" for="MyModel">
      <old-form merge multipart>
        <field-list: fields="photo, other-fields, ..."/>
      </old-form>
    </extend>

### License

See MIT-LICENSE

