# getitem
- Magic method which gets exexuted when, class variable is passed key
- Provides a functionality by which class behave as a dictionary.

```python
class HelperClass:
    
    def __init__(self):
        self.d = {'name':'surya'}

class MyClass:
    
    def __getitem__(self,key):
        h = HelperClass()
        return getattr(h,key)
        

m = MyClass()
print(m["d"])
```
**Outpur:** ``{'name':'surya'}``

> Note: getattrib(cls,attrib_name) is used to get the attribute of the class.

