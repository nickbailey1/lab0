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
Occasionally, the first test fails, with an assertion error that indicates the process
count was off by one (every failure has only  been off by one). To the best of my
knowledge, my code handles process counting the way the assignment intends it to be
handled, and this error is likely due to a race condition between when the kernel module reads the process count
and when the python test reads the process count. This could be due to the python test
or interpreter itself, or some other process starting or ending between the time that
the test reads /proc/count and when it independently checks the process count. Alternatively, it could be a product of the environment I'm programming on, which is an M1 Macbook Pro (ARM architecture) emulating the x86 architeture in the VM. According to some quick research, the scheduler behavior can differ between native hardware and a virtualized environment, which could be another potential explanation.

Report which kernel release version you tested your module on
(hint: use `uname`, check for options with `man uname`).
It should match release numbers as seen on https://www.kernel.org/.

```shell
uname -r -s -v
```
Kernel release version: Linux 5.14.8-arch1-1 #1 SMP PREEMPT Sun, 26 Sep 2021 19:36:15 +0000