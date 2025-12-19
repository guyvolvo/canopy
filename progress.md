In here I will be documenting my progress as I go and learn new things \
```python

import json

with open('platforms.json', 'r') as f :
    data = json.load(f)

platforms = data['platforms']

username = 'guyvolvo'
for platform_name , platform_info in platforms.items():
    url = platform_info['url'].format(username)
    print(f"{platform_name}: {url}")

```
