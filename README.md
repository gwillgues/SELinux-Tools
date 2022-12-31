# SELinux-Tools
My collection of SELinux related Software/Policies/etc that make my life easier in managing SELinux.

# compilete
**How to compile a .te file into .pp:**

Sometimes audit2allow will fail to generate a valid .te file, which results in compilation errors. After modifying the .te to be valid, you can manually compile it with `checkmodule` and `semodule_package` , but this takes up time.

compilete will take a filename as the first argument and attempt to compile any .te files with that name in the current directory. For example: `compilete myModule.te`. It will output a .mod and .pp file with the same name as the .te . If the .pp file is successfully generated, you can load it with `semodule -i myModule.pp` 


This saves a ton of time from looking at the `audit2allow` man page to find the checkmodule and semodule_package syntax for manual compilation, as well as having to type those commands out. 

Place in `/usr/bin/compilete` for best usage.

# domtrans_example.txt
When making custom SELinux policies, I ran into an issue where a custom SELinux policy was launching under context of the parent process and was not properly transitioning. When checking the AVC denials in the audit log, you will see the parent process requesting "execute_no_trans" on the custom type
you created.

This example shows what you need to add to your .te file before you compile it to force the transition to the proper policy.
