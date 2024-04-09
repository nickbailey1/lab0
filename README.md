# A Kernel Seedling
An introduction to kernel modules in Linux. In this lab, I completed a C program that uses Linux's seq_file API to output the number of processes running, directly from the kernel. The module can be built from source using a Makefile routine, and then inserted into the kernel. The output of the program is generated when /proc/count is read by cat, which cat then outputs.

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
```shell
sudo rmmod proc_count.ko
```
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
Kernel release version: Linux 5.14.8-arch1-1 #1 SMP PREEMPT Sun, 26 Sep 2021 19:36:15 +0000