## 1. Loading Image into the template from the model

```html
<img src="{{context_obj_name.image_field_name.url}}" class="img-fluid"/>
```
**Note** .url.

## 2. Getting the context variable in the class based views

```python
from django.view.generic import ListView, DetailView

.....

class FooListView(ListView):

  def get_context_data(self, *args, **kwargs):
    """Get the context data"""
    
    context = super(FooListView, self).get_context_data(*args, **kwargs)
    context["key"] = value # assign value to context variable
    
    return context
```
