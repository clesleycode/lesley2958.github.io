This site has been modified to the blog at lesley2958.github.io

Original: 

# Blog Address

<http://blog.rainyalley.com/>


# Must Modify

## 1.swiftype

This service provides the on-site search function.

Service address： <https://swiftype.com/>.

After the setup is complete， you need to modify the `swiftype_searchId` in `_config.yml`.

In your swiftype engine, go to `Setup and integration` -> `Install Search`, you could find the `swiftype_searchId`.

```html
<script type="text/javascript">
...
...
  _st('install','swiftype_searchId','2.0.0');
</script>
```
