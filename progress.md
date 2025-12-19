### **In here I will be documenting my progress as I go and learn new things**
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

Figuring out how to actually use the json file I created and print out all the platforms on there with my name 

<img width="552" height="323" alt="image" src="https://github.com/user-attachments/assets/82427a60-4335-4044-ba5d-2abb5242a6f6" />

Works fine,

Now I will probably be using argparse in this project like I did with my directory enumerator since I really like how it turned out \
These are all the arguments I've decided to include in the framework

```python
import json
import argparse


def main():
    parser = argparse.ArgumentParser(
        description='Canopy - Username Enumeration Tool',
        formatter_class=argparse.RawDescriptionHelpFormatter,
        epilog="""
    Examples:
      canopy -u johndoe
      canopy -u johndoe -t 50 --timeout 15
      canopy -u johndoe -o report.json --format json
      canopy -u johndoe --categories social,gaming
      canopy --list-categories
            """
    )
    # Target group
    target_group = parser.add_argument_group('Target Options')
    target_group.add_argument('-u', '--username', help='Username to search for', type=str)
    target_group.add_argument('-U', '--usernames', help='File containing list of usernames (one per line)', type=str)

    # Performance group
    performance_group = parser.add_argument_group('Performance Options')
    performance_group.add_argument('-t', '--threads', help='Number of concurrent threads (default: 10)', type=int,
                                   default=10)
    performance_group.add_argument('--timeout', help='Request timeout in seconds (default: 10)', type=int, default=10)
    performance_group.add_argument('--delay', help='Delay between requests in seconds (default: 0)', type=float,
                                   default=0)
    performance_group.add_argument('--rate-limit', help='Max requests per second (default: unlimited)', type=int,
                                   default=None)
    # Filter group
    filter_group = parser.add_argument_group('Filtering Options')
    filter_group.add_argument('-c', '--categories', help='Comma-separated categories to check (e.g., social,gaming)',
                              type=str)
    filter_group.add_argument('-p', '--platforms', help='Comma-separated specific platforms to check', type=str)
    filter_group.add_argument('--exclude', help='Comma-separated platforms to exclude', type=str)
    filter_group.add_argument('--only-found', help='Only show found accounts', action='store_true')

    # Output group
    output_group = parser.add_argument_group('Output Options')
    output_group.add_argument('-o', '--output', help='Output file path', type=str)
    output_group.add_argument('-f', '--format', help='Output format: json, csv, html, txt (default: json)', type=str,
                              choices=['json', 'csv', 'html', 'txt'], default='json')
    output_group.add_argument('-v', '--verbose', help='Verbose output', action='store_true')
    output_group.add_argument('-q', '--quiet', help='Minimal output (only results)', action='store_true')
    output_group.add_argument('--print-found', help='Print found accounts in real-time', action='store_true')
```
