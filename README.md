# Semantic Form Builder

Semantic Form Builder is a customer FormBuilder for use in Rails, aiming to
give accessible, consistent, forms with the ultimate of DRY.

No more defining labels, worrying about formatting, etc. Let the default
form_for tag take care of all the hassles for you

For an example of what it looks like check:
http://rubypond.com/articles/2008/07/16/sexy-forms-in-rails/

## Installation

```term
$ script/plugin install git://github.com/rubypond/semantic-form-builder.git
$ rake semantic_form_builder:setup # (if the installation script didn't move the semantic_form.css into /public/stylesheets/)

1. If you wish to use the builder to replace the default for all forms (which is great for consistency) then add the following into an initializer `ActionView::Base.default_form_builder = SemanticFormBuilder`. Otherwise pass the builder in as the `:builder` parameter for `form_for`.
2. Be sure to include `semantic_forms.css` in your layout

## Usage

Continue using form_for and the tag helpers within it as you did before and it should work fine. There has been a few additional tags added for convenience sake. They are:

* `submit_and_cancel`
* `radio_button_group`
* `check_box_group`

More documentation on their usage to come, in the interim check out or the http://rubypond.com/articles/2008/07/16/sexy-forms-in-rails/ following example:

```erb
<% form_for @document do |f|
  field_set_tag "Form Details" do %>
    <%= f.date_select :date, :required => true, :help => "date the something happened" %>
    <%= f.text_field :number, :required => true, :help => "the reference number for this thing" %>
    <%= f.select :external_id, [["Choose an option...",""]] + @externals.map{|c| [c.name, c.id]}, :required => true, :label => "options", :help => "select something from the list" %>
    <%= check_box_tag_group "document[other_items][]", @others.map{|u| { :value => u.id, :label => u.description }}, :label => "including these?", :help => "tick the whatever boxes are appropriate for this&nbsp;thing" %>
    <%= f.text_field :name, :help => "what was Willis talkin' about?" %>
    <%= f.check_box :list, :label => "mailing list", :help => "can we send you a bunch of spam?" %>
    <%= f.submit_and_cancel("save", "cancel") %>
<% end %>
```

[![Analytics](https://ga-beacon.appspot.com/UA-46840117-1/semantic_form_builder/readme?pixel)](https://github.com/igrigorik/ga-beacon)
