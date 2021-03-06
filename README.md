# DriverStoreCleaner
Explore Windows System Driver Store and Cleanup old drivers

DriverStoreCleaner makes it easier to clean up Windows 7 [driver store](https://msdn.microsoft.com/en-us/library/ff544868(v=vs.85).aspx).

This project is inspired by and uses ideas from:

* [DriverStore Explorer [RAPR]](https://driverstoreexplorer.codeplex.com/) by [Kannan Ramanathan](https://www.codeplex.com/site/users/view/kannanmr)

  > DriverStoreExplorer GUI makes it easier to deal with Windows Vista / Windows 7 driver store.
  Supported operations include enumeration, adding a driver package (stage), adding & installing,
  deletion and force deletion from the driver store.

  DriverStoreExplorer is written in C# and uses `pnputil` for enumeration, info retrieving and
  safe deletion of the drivers. So, the info fields of a driver shown are INF-file, Pkg Provider,
  Driver Class, Date, Version and Signer.

* [pyWinClobber/driver_cleanup.py](https://github.com/JustAMan/pyWinClobber/blob/master/driver_cleanup.py)
and [this article](http://habrahabr.ru/post/196404/) by [JustAMan](https://github.com/JustAMan)

  > This script performs DriverStorage cleanup removing possible staged driver duplicates.
The operation should be safe as it utilizes MS pnputil.exe to do the job, and the mode
in which the util is used forbids removing the driver that is currently used for installed
devices.

  driver_cleanup.py is written in Python and uses `pnputil` for enumeration, info retrieving
  and safe deletion of the drivers, too. But it uses some advanced techniques to estimate the size
  occupied by a driver in the Driver Store, and to determine the latest driver and old drivers
  for a device. A user can find out by that how much space would be freed and can automatically
  delete old drivers.

* [PnpFind](https://github.com/mcuee/PnpFind) by [mcuee](https://github.com/mcuee)

  > pnpfind Vista/7 driver storage managment console program by Travis Robinson

  PnpFind is written in C# and uses File API for enumeration,
  [Windows SetupAPI](https://msdn.microsoft.com/en-us/library/cc185682(v=vs.85).aspx) for info retrieving
  and `pnputil` for forced deletion of the drivers.

The goal of this project is to make a GUI interactive program with the functionality of the console script
[driver_cleanup.py](https://github.com/JustAMan/pyWinClobber/blob/master/driver_cleanup.py) and to add
the ability of removing the drivers that
[pnputil](https://msdn.microsoft.com/en-us/library/windows/hardware/ff550419(v=vs.85).aspx) does not detect.

It happens when the OEM INF file of a driver has been removed, but the driver remains staged in the Driver Store.
In that case, one can use [dism](https://msdn.microsoft.com/en-US/library/hh825258.aspx) utility to get an
extended list of drivers in the Driver Store. So after that, to get `pnputil -d` working, we should find
the corresponding INF file and copy it to the Windows INF directory.

That's the feature that the above projects don't implement.
