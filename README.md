# What is this?

I wanted a light, clean, configurable alternative to tqdm. So I made one.

It with jupyter notebooks and regular python.

# How do I use this?

`pip install informative_iterator`

```python
from informative_iterator import ProgressBar
import time

# 
# example 1
# 
for progress, each in ProgressBar(range(1000)):
    time.sleep(0.01)
# example output:
# [>..................................]  0.00% |    0/1000 | started: 13:18:32 | eta: ________ | remaining: ________ | 
# example output:
# [==============>....................] 42.50% |  425/1000 | started: 13:18:32 | eta: 13:18:44 | remaining: 0:07sec | 
# example output:
# [================================>..] 93.10% |  931/1000 | started: 13:18:32 | eta: 13:18:44 | remaining: 0:01sec | 
# example output:
# Done in 0:12sec at 13:18:44

# 
# example 2
# 
import random
def custom_iterable():
    yield random.random()

for progress, each in ProgressBar(custom_iterable(), total=1000):
    time.sleep(0.01)

# 
# example 3
# 
for progress, each in ProgressBar(1000):
    time.sleep(0.01)
    # index, just like using enumerate()
    print('progress.index   = ', progress.index)
    # percent with two decimal places. ex: 99.5
    print('progress.percent = ', progress.percent)
    # the output of time.time() for this iteration (seconds since unix epoch)
    print('progress.time    = ', progress.time)
    # boolean (updates dont always get printed every iteration)
    print('progress.updated = ', progress.updated)
    # int, doesn't change with iterations: its the size of the iterator
    print('progress.total   = ', progress.total)

# 
# example 4
# 
# update ~30 times a second for smooth looking progress
for progress, each in ProgressBar(1000, seconds_per_print=0.03):
    time.sleep(0.01)

# 
# example 5
# 
# have all progress bars default to trying to update update ~30 times a second
ProgressBar.configure(
    seconds_per_print=0.03,
)
for progress, each in ProgressBar(1000):
    time.sleep(0.01)

# 
# example 6
# 
ProgressBar.configure(
    # all the options (these exist as arguments for ProgressBar as well)
    layout=[ 'title', 'bar', 'percent', 'spacer', 'fraction', 'spacer', 'start_time', 'spacer', 'end_time', 'spacer', 'remaining_time', 'spacer', ],
    spacer=" | ",
    minmal=False, # defaults to normal layout
    minimal_layout=[ 'title', 'bar', 'spacer', 'end_time', 'spacer', ],
    inline=True,
    disable_logging=False, # turn off all the output
    progress_bar_size=35,
    seconds_per_print=1, # print every second
    percent_per_print=10, # And print every 10% of progress
)
for progress, each in ProgressBar(1000):
    time.sleep(0.01)
```
