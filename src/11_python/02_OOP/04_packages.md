# Packages #

1. Create new package
2. Create new file with name __init__.py
3. Create new module in the package
4. Import package function to app.py in the different place of project

app.py
```python
import package_name.file_name

package_name.file_name.function_name
```
or 

app.py
```python
from package_name.file_name import function_name

function_name()
```

or 

app.py
```python
from package_name import file_name

file_name.function_name()
```