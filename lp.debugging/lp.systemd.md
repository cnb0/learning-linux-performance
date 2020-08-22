
## [systemd]https://lzone.de/cheat-sheet/systemd)

```
- The default system and service manager for most Linux distributions now is systemd

- The systemd process replaces the SysV init. 
- It runs as the first process after the kernel boot 
- is responsible for bringing the Linux host up to the state where it can be used. 
- It is responsible for starting and managing the 
        - services, 
        - mounting filesystems, 
        - managing hardware, 
        - generating the login prompt etc

- A key benefit over SysV is that systemd starts as many services as possible in parallel, 
   thus speeding up the startup process, and that brings up the login screen faster.

- Units
    - The items that are managed by the systemd are called units. 
    - The unit files are located in /lib/systemd/system.

- Service Units
    -  For service management, the target units are service units,
       which have unit files with a suffix of .service.
- Managing systemd services

    - To start a systemd service, use the systemctl start command:
        $ sudo systemctl start name.service

    - Viewing System State
        $  sudo systemctl -t help

    - To list all installed units, use list-unit-files
        $ sudo systemctl list-unit-files

        - The output has only two columns Unit File and State. 
        - The state will usually be enabled, disabled, static or masked.
        - Static: 
            - This means the unit cannot be enabled, performs a one-off action, or 
              is a dependency of another unit and cannot be run by itself.
            - Masked: 
                - A unit listed as masked means it is completely unstartable, as it is linked to /dev/null. 
                - This is called masking the unit. This prevents the service from being started, manually or automatically.
    - List all installed services
        - The systemctl list-unit-files command with -t or –type service 
          filter shows the state of installed services only.
            $ sudo systemctl list-unit-files -t service

    - To see all active service units, use list-units with -t service filter
            $ sudo systemctl list-units -t service

                - The output has the following columns :
                    UNIT: The systemd service unit name
                    LOAD: Shows whether the unit definition was properly read and loaded
                    SUB: Low-level activation state of the unit, giving more detailed information about the unit. 
                    This will vary by unit type.
                    DESCRIPTION: The service unit’s description.