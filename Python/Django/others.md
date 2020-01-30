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

## Runing Django Dev Server on local Wi-Fi network

**i. Get the ip of local machine**

``ifconfig``

**ii.Grab the ip:**

```
wlp2s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.70(Local Machine IP)  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::dbd9:d99f:c6f9:feb7  prefixlen 64  scopeid 0x20<link>
        ether 2c:6e:85:ee:54:a8  txqueuelen 1000  (Ethernet)
        RX packets 19656  bytes 21227997 (21.2 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 8552  bytes 1839939 (1.8 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

**iii. Open the port 8000 for accessing django on dev machine:**

``sudo ufw allow 8000/tcp``

**iv. Allow all ip in django HOST lists**
```python
ALLOWED_HOSTS = ['*']
```

**v. Launch server from local machine ip and port**

```python
python manage.py runserver <local_machine_ip>:<allowed_port>
```
