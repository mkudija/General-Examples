# Sleep

To sleep for a random amount of time (i.e. between web scraping requests):

```python
from time import sleep

def random_time(mu, sigma):
    s = np.random.normal(mu, sigma, 1)
    return max(s[0],2.5)

for i in range(4):
    # sleep
    s = random_time(mu=28,sigma=13)
    print('\tWaiting {:.2f} seconds...'.format(s))
    sleep(s)
    i+=1
```
