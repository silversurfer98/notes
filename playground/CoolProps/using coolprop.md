- this is a python pip package

> documentation old --> [link](http://www.coolprop.org/v4/apidoc/CoolProp.html)

```python
import CoolProp
import CoolProp.CoolProp as cp

print('CoolProp version: ', CoolProp.__version__)
print('CoolProp gitrevision: ', CoolProp.__gitrevision__)
print('CoolProp fluids: ', CoolProp.__fluids__)

#usage
den = cp.PropsSI('D', 'P', p, 'Q', 1, 'Water')
```