everytime we passed a file as parameter to the ./flracing, it stated-> file unchanged. Good luck next time kiddo!.

After trying upon random linux commands like strings, we stumbled upon a random idea to change the file on loop while it's being read by the program. We wrote a python script to change the file every 0.1 seconds. 

```python
import os
import time

while True:
    # open new.txt file
    with open('new.txt', 'a') as f:
    # edit content of new.txt
        f.write("Hello World")
    # close the file
    f.close()
    time.sleep(0.001)
```

After running the script, we ran the ./flracing and the flag was printed on the terminal.

Flag is HR24{0383d4bd9ad8ddfc53c24aa6c4bdbc8a}
