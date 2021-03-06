## 1. Loading Image into the template from the model

```html
<img src="{{context_obj_name.image_field_name.url}}" class="img-fluid"/>
```
**Note** .url.

## 2. Passing variables to Templates

**Templates/base.html**

```html
  {%include 'base/another_template.html' with someVariable%}
```

**Note:** ``with someVariable``

**Base/another_template.html**
```html
<h1>{{someVariable}} </h1>
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
> Note the usage of ``Foo.objects.get`` 

**Another way of handling exception when there exists two or more objects satisfying the certain criteria**
```python
qs = Foo.objects.filter(title=query)
if qs.exists() and qs.count() == 1:
  instance = qs.first() 
else:
  raise Http404("Foo doesn't exists.")
```
**Note:** ``instance = qs.first()``

### c. Others

**Creating objects for ManyToManyField**
- Direct method
```python
  pro = Product.objects.create(..........)
  pro.attributed.create(color=prod_attr[0],size=prod_attr[1],stock= prod_attr[2])
  pro.save()
```
- By Referencing to the object
```python
foo = Foo.objects.create(....)
bar = Bar.objects.get(...)
bar.M2MFieldName.add(foo)
```

### D. Date Filtering In between range

```python
inv = Invoice.objects.filter(supplier=custom, invoice_date__date__range=[entry_date, end_date])
```
