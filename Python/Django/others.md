## Custom Manager Vs Custom Querysets

**Source:** [Stackoverflow](https://stackoverflow.com/questions/29798125/when-should-i-use-a-custom-manager-versus-a-custom-queryset-in-django)

Mainly to allow for easy composition of queries. Generally if you want to be able perform some operation on an existing queryset in a chain of queryset calls you can use a `QuerySet`. 

For example, say you have an `Image` model that has a `width`, `height` fields:

```python
    class Image(models.Model):
        width = ...  # Width in pixels
        height = ... # Height in pixels
```

you could write some custom `QuerySet` methods: 

```python
    class ImageQuerySet(models.QuerySet): 
        def landscapes(self):
            return self.filter(width__gte=models.F('height'))

        def portraits(self):
            return self.filter(width__lte=models.F('height'))

        def small(self):
            return self.filter(width__lte=1200)

        def large(self):
            return self.filter(width__gte=1200)

    class ImageManager(models.Manager):
        def get_queryset(self):
            return ImageQuerySet(self.model, using=self._db)
```

now you can easily create dynamic querysets:

```python
    Image.objects.all().portraits().small()
    Image.objects.all().large().portraits()
```
Logically, these functions should be concerned primarily with partitioning or redefining of existing querysets of the queryset's model. For situations where you aren't operating on existing querysets, you don't want to return a queryset at all, or you might have to perform some related logic that doesn't involve this particular model, than a model manager it better suited. 
