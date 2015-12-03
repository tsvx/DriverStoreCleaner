# DriverStoreCleaner
Explore Windows System Driver Store and Cleanup old drivers

DriverStoreCleaner makes it easier to clean up Windows 7 [driver store](https://msdn.microsoft.com/en-us/library/ff544868(v=vs.85).aspx).

This project is inspired by and uses the ideas from:
* [DriverStore Explorer [RAPR]](https://driverstoreexplorer.codeplex.com/)
* [pyWinClobber](https://github.com/JustAMan/pyWinClobber) and [this article](http://habrahabr.ru/post/196404/)
* [PnpFind](https://github.com/mcuee/PnpFind)
 
The goal is to make a GUI-version of the console script [driver_cleanup.py](https://github.com/JustAMan/pyWinClobber/blob/master/driver_cleanup.py) and to add the ability of removing old drivers that [pnputil](https://msdn.microsoft.com/en-us/library/windows/hardware/ff550419(v=vs.85).aspx) does not detect.

It happens when the oem inf-file of a driver is removed, but the driver remains staged in the Driver Store.
In that case, one can use [dism](https://msdn.microsoft.com/en-US/library/hh825258.aspx) utility to get extended list of drivers in the Driver Store. So after that, to get `pnputil -d` working, we should find the corresponding inf-file and copy it to the Windows Inf directory.

That's the feature that the above projects don't implement.
