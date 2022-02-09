# SELinux-Tools
My collection of SELinux related Software/Policies/etc that make my life easier in managing SELinux.

# compilete
**How to compile a .te file into .pp**
Sometimes audit2allow will fail to generate a valid .te file, which results in compilation errors. After modifying the .te to be valid, you can manually compile it with `checkmodule` and `semodule_package` , but this takes up time.

compilete will take a filename as the first argument (without the .te file extension) and attempt to compile any .te files with that name in the current directory. For example: `compilete myModule`. It will output a .mod and .pp file with the same name as the .te . If the .pp file is successfully generated, you can load it with `semodule -i myModule.pp` 


This saves a ton of time from looking at the `audit2allow` man page to find the checkmodule and semodule_package syntax for manual compilation, as well as having to type those commands out. 

Place in `/usr/bin/compilete` for best usage.
