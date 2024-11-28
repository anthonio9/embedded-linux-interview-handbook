## Embedded Linux

* Linux Kernel API:
    - the "kernel–user space" API - make kernel resources available in the userspace
    The system calls are gathered in this manual: https://man7.org/linux/man-pages/man2/syscalls.2.html | man 2 syscalls
    - the "kernel internal" API.

* Namespaces 

* Mutex vs Semaphor
    - semaphors are used for synchornization, binary semaphors are just an integer
    - Binary Semaphores have two operations namely wait(P) and signal(V) operations. Both operations are atomic.
    - mutexes are used to protect shared resources. A mutex is owned by the 
    - A mutex can be released only by the thread that had acquired it. 
    - examples:
        * mutex: one uart, two threads printing to it. thread that locks mutex is the one to release it after printing to said uart. 
        technically another thread can unlock if it has a reference to the mutex, but this is undefined behavior and poor design.

        * semaphore: one thread waiting on some event, blocks on a semaphore. 
        with the same uart analogy, an ISR signals the semaphore to wake the blocked thread saying that there's data in some buffer. 
        thread wakes up, processes data, blocks on the same semaphore again.

* What is /sbin/init

* How do you configure and build a Linux kernel for an embedded system?
    - Download the kernel source from the official website
    - Configure the kernel using the configuration tool (e.g. make menuconfig)
    - Set the configuration options to match the target system requirements
    - Compile the kernel and build the image (e.g. make zImage)
    - Create a bootloader image (e.g. U-Boot)
    - Copy the kernel image to the boot partition of the target device
    - Copy the bootloader image to the boot partition of the target device
    - Reboot the device and boot from the new kernel image

* What is the role of the bootloader in an embedded Linux system?
    The bootloader is responsible for initiating the boot process in an embedded Linux system. 
    It is responsible for loading the operating system kernel into memory and starting the kernel.
    Additionally, it can provide a user interface for configuring the system, such as selecting a different kernel or boot device.
    The bootloader is usually the first piece of code that is executed when the system is powered up or reset.

* How can memory be allocated in the kernel drivers / kernel API
    kmalloc - physical memory, vmalloc - virtual memory

* List a few filesystems often used in the embedded linux world:
  - ext2
  - cramfs
  - JFFS2
  - squashfs
  - YAFFS2
  - [seemingly great article on the filesystems](https://www.linkedin.com/pulse/some-common-file-systems-embedded-linux-mohammad-t-abdoli/)

* Explain the difference between UART, SPI and I2S
