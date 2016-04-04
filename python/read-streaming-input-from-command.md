# Read Streaming Input From Shell Command

To read the stdout of a subprocess within a python script you can use the [subprocess](https://docs.python.org/2/library/subprocess.html) module with `subprocess.PIPE` like so:

```python
process = subprocess.Popen(command, stdout=subprocess.PIPE, shell=True)
    while (process.poll() is None):
        output = process.stdout.readline()
```
