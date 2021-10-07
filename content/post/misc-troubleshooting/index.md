---
title: Miscellaneous Troubleshooting Tricks

# Summary for listings and search engines
summary: In this post we will present some useful hacks that I found useful in troubleshooting various things.

# Link this post with a project
projects: []

# Date published
date: "2021-10-07T00:00:00Z"

# Date updated
date: "2021-10-07T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags: [troubleshooting, tricks, hacks, howtos. python, java, pandas, programming, ml]


categories:
- How-to
---

### Fixing `_csv.Error: field larger than field limit (131072)`

**Solution**: We need to increase `csv.field_size_limit`. The following code snippet shows the configuration how to increase default csv field limit. **Note**, this technique is also useful if you run into this issue while workding with Panda's `pd.read_csv()` method as well.

```python
import csv
#if you're not sure what'd be the maximum field size, use system maxsize
field_size_limit = sys.maxsize

while True:
    try:
        csv.field_size_limit(field_size_limit)
        break
    except OverflowError:
        field_size_limit = int(field_size_limit / 10)
```

