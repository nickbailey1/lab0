# A Kernel Seedling
TODO: intro

## Building
```shell
make
```

## Running
```shell
sudo insmod proc_count.ko // inserts the module into the kernel
cat /proc/count // outputs the contents of the virtual file
```
Simply prints the number of processes that are running.

## Cleaning Up
```shell
make clean
```
when building the binary again, you will have to remove the kernel from the module with:
'''shell
sudo rmmod proc_count.ko
'''
and then reinsert it.

## Testing
```python
python -m unittest
```
The unittest outputs that it ran 3 tests, and the time it took. Then it says OK.

Report which kernel release version you tested your module on
(hint: use `uname`, check for options with `man uname`).
It should match release numbers as seen on https://www.kernel.org/.

```shell
uname -r -s -v
```
TODO: kernel ver?