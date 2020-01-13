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

## 3. Django QuerySet vs Get Specific Instance
- Exception Handling is must during the execution of CRUD operation
#### a. Getting queryset
- Returns the set of an objects matching the certain criteria.

```python
qs = Foo.objects.all() # returns all the objects from Foo model
qs = Foo.objects.filter(id=query)
```

#### b. Getting the specific instance
- Return the specific instance 

```python
instance = Foo.objects.get(id=query)

# handling the exception
from django.shortcuts import get_object_or_404

instance = get_object_or_404(Foo, id=query)

# using try catch
from django.http import Http404

try:
  instance = Foo.object.get(id=query)
except Foo.DoesNotExist:
  raise Http404("Foo Doesn't exists")
```
**Another way of handling exception, queryset for search operation**
```python
qs = Foo.objects.filter(title=query)
if qs.exists() and qs.count() == 1:
  instance = qs.first()
else:
  raise Http404("Foo doesn't exists.")
```
