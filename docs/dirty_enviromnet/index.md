# Dirty Environment


Sometimes MDT deployments fail and leave the disk in a dirty (failed) state, whem you choose yes and the task sequence failes try the following solution.

1.	Press F8 (opens a CMD window)

2.	Unplug any USB drives or other mass storage devices - you should end up with just the internal hard drive left (CD/DVD drives don't count here)

3.	In the CMD window enter: DiskPart (launches the Disk Partitioning window)

4.	In the DiskPart window enter: list disk (this will show you a list of discs available)

5.	If all other drives were unattached then only 1 disk will be listed - note the number associated with the disk (most likely it will be ZERO)

6.	In the DiskPart window enter: select disk # (where # is your disc number)

7.	In the DiskPart window enter: clean (this will wipe the disk clean of all partitions and therefore clear your dirty deployment)

8.	In the DiskPart window enter: exit (should close)

9.	In the CMD window enter" exit (should close and reboot)

![Dirty Environment](/images/dirtyenvironment.jpg)


---

> Author: Raymond Zaagsma  
> URL: https://raymondzaagsma.github.io/dirty_enviromnet/  

