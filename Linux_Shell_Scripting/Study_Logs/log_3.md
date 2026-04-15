# Date: 22-01-2026
## Topics:
- what is operating system
    - resource manager
    - virtualisation: illusion which OS simulates by the process it has access to complete hardware resource
        - infinite storage
        - complete access to CPU
    - Process Management:
        - Manages concurrency,syncronisation
            - context switching
            - managing PCB
            - Scheduling process
    - Memory Management:
        - virtual addresses
        - syncronisation: mutex locks to prevent one process/thread access a memory block at a time
    - Storage Mangement:
        - manages serialisation and deserialisation 
        - file system
        - manage persistency
    - Device Management:
        - Manage access to devices: i/o,external devices
            - Like keyboard,speaker,microphone,monitor,usb,printer
    - Security:
        - manage access to resources
        - manage users and permission

- How OS is madeup:
    - Kernel
    - system calls
    - Device drivers
    - application layer
    - user application
    - Architecture and working

- What is POSIX
    - reason for similarity between working macos and linux


- What is virutalisation
    - Virtual macine: is basically a machine which can run isolately like sole machine
        - Virtual means: It doesn't have it's own hardware it uses hardware of another machine on which it is installed
        - It uses hardware of host machine
        - To use the hardware of host machine we need a software which monitors resource utilisation and creates a illusion for VM which it has access to complete hardware: This software is called(Hypervisor)
        - Used for testing software on different environments
        - It is isolated and also increase the resourcability of a machine
        - It allows efficient usage of hardware resources
        - How virtualisation was developed what is causality?
            - Portability and fault-tolearance
    - Types of Hypervisor:
        - Type-1: More light-weight and less overhead
        - Type-2: More overhead needs to syncronise and communicate with host OS
