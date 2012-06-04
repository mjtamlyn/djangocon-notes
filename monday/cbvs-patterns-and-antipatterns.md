# CBVs: Patterns and AntiPatterns

## [Bruno Renie](http://twitter.com/brutasse)

- Author of django-floppy-forms. (HTML5 widgets)

- New in 1.3, better in 1.4
- Controversial! Luke Plant's blog post...

### What defines a view?

- A callable which takes a request and gives a response.
- Function generic views are going away. Functional views full stop are
  **NOT**.
- Other class based stuff? Middleware, Admin... Single class instance shared
  across request
- Inherit from base view and call `.as_view()`. This instantiates the view
  class on every request. It's important! Allows us to store stuff on self.
- Declarative vs imperative. More extensibility for less simplicity.
- ccbv.co.uk

### (Biased) usage tips

- Keep urls.py for URLs. Decorate in views.py.
- CBV decorator. That one was slightly different - should look into it.
- Or use mixins, or maybe not. But good for things with config, like cache.
- MRO: Extend, don't override (unless you know 100% what you're doing). Use
  super everywhere.

### Case studies

- Form processing. Let the form itself deal with everything - not so much with
  the view. Override `form_kwargs`, and then call `save` (even if not a
  ModelForm)
- Navigation levels
- Easy to reuse bits of code

### Registration

django-registraition is great but... We want to do (insert blah here).
Investigate `django-le-social`. Nicer views that do other things.

### Settings

I'll add a setting! STOP!

- Does it have to be global?
- Could people want to switch it at any time?
- Could it be a class method instead?

For example the registration email confirm timeout. Override the view and set
the class attribute instead of using a setting. (and other examples)

### CBVs are not the answer to everything

- e.g. ``Handler500(TemplateView)``. Ooops, no POST method.
- Don't limit yourself to the django generic views. Use the base view, some
  mixins and a load of creativity.
