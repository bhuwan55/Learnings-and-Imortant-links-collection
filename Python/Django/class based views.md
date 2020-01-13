## 1. Getting the context variable in the class based views

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