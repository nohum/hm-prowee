# hm-prowee
Communicate with Homegear server over XML-RPC

## Usage

    hm-prowee -u <user> -s <server> -p <port> list
    hm-prowee -u <user> -s <server> -p <port> print-config <id>
    hm-prowee -u <user> -s <server> -p <port> set-temp <id> <file>

The `-u <user>` is the user created in homegear to connect to, see [Homegear Documentation](https://www.homegear.eu/index.php/Create_or_Delete_Users_Using_Homegear%27s_Command_Line_Interface). The `-s <server>` specifies to which server the connection should be done and with `-p <port>` the connection port is defined.
The server should be specified as hostname (`homegear.local`, or `192.168.1.1`), not in URL Syntax (like "http://example.com"). When launching the command the password for the connection will be asked.

The `list`-command with list all devices with type "0x95", which means the "HM-CC-RT-DN"-Devices.

The `print-config` will print the actual config of the `<id>`.

The `set-temp` command will then set the device with the `id` the temperature config from the `file`. For the syntax of the file see below.

## Syntax of the Temperature file

Example file:

    MONDAY = 17.0 > 15:00; 20.0 > 19:00; 19.0 > 24:00;
    TUESDAY = 17.0 > 15:00; 20.0 > 19:00; 19.0 > 24:00;
    WEDNESDAY = 17.0 > 15:00; 20.0 > 19:00; 19.0 > 24:00;
    THURSDAY = 17.0 > 15:00; 20.0 > 19:00; 19.0 > 24:00;
    FRIDAY = 17.0 > 15:00; 20.0 > 19:00; 19.0 > 24:00;
    SATURDAY = 17.0 > 09:00; 19.5 > 19:00; 19.0 > 24:00;
    SUNDAY = 17.0 > 10:00; 19.5 > 19:00; 19.0 > 24:00;

The lines should start with the day of week. It should be uppercase.

After the equal sign there can be 13 sets temperature intervals. This number is limited by the device itself.

The sets should be read as `<temperature> until <time>`. The first interval starts at 00:00. So the line for "MONDAY" reads as "set 17°C until 15:00, then set it to 20°C until 19:00, then 19°C until 24:00". The last set should always last until 24:00. The intervals should be consecutive.
There no checking included in the script (yet)!
