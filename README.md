# SMS Modem Manager

SMS Modem Manager is a Python script that provides a command-line interface for interacting with a GSM modem. It allows you to send, receive, and manage SMS messages directly from your terminal.

## Features

- Send SMS messages
- Check received SMS messages
- Delete individual or all SMS messages
- Quiet mode for easy integration with other scripts
- Configurable modem port and baud rate

## Requirements

- Python 3.6+
- pyserial library

## Installation

1. Clone this repository or download the `smsmanager` script.
2. Install the required Python library:

   ```
   pip install pyserial
   ```

3. Make the script executable:

   ```
   chmod +x smsmanager
   ```

4. (Optional) Move the script to a directory in your PATH for easy access:

   ```
   sudo mv smsmanager /usr/local/bin/
   ```

## Usage
```
usage: smsmanager [-h] [-q] [--port PORT] [--baudrate BAUDRATE]
                  {send,check,delete,help} ...

Modem SMS Operations - Interface with a modem for sending, checking, and deleting SMS messages.

positional arguments:
  {send,check,delete,help}
                        SMS operations
    send                Send an SMS message
    check               Check and display all received SMS messages
    delete              Delete a specific SMS message or all messages
    help                Show this help message and exit

optional arguments:
  -h, --help, -?        Show this help message and exit
  -q, --quiet           Output in quiet mode (for use with other programs)
  --port PORT           Modem port (default: /dev/modemAT)
  --baudrate BAUDRATE   Baud rate (default: 115200)

Example usage:
  smsmanager send "+1234567890" "Hello, world!"
  smsmanager check
  smsmanager check -q
  smsmanager delete 1
  smsmanager delete all
  smsmanager --port /dev/ttyUSB0 --baudrate 9600 send "+1234567890" "Custom port and baudrate"
```


### Sending an SMS


```
root@raspberrypi:/usr/local/bin# smsmanager send "+1234567890" "Your message here"
SMS sent successfully to +1234567890
```

### Checking received messages

```
root@raspberrypi:/usr/local/bin# smsmanager check
Received messages:
======================================================================
Message ID: 0
Status: REC READ
From: +1234567890
Timestamp: 23/05/06,14:30:45+00
Content:
This is a test message. It can be multiple lines long and will be
wrapped automatically to fit the display.

======================================================================
Message ID: 1
Status: REC UNREAD
From: +9876543210
Timestamp: 23/05/06,15:45:30+00
Content:
Another message from a different sender.

```

Quiet mode (for use with other programs):

Command:
```
root@raspberrypi:/usr/local/bin# smsmanager check -q
MESSAGE[0]="This is a test message. It can be multiple lines long and will be wrapped automatically to fit the display."
TIME[0]="23/05/06,14:30:45+00"
SENDER[0]="+1234567890"
STATUS[0]="REC READ"
INDEX[0]="0"
MESSAGE[1]="Another message from a different sender."
TIME[1]="23/05/06,15:45:30+00"
SENDER[1]="+9876543210"
STATUS[1]="REC UNREAD"
INDEX[1]="1"
```

### Deleting messages

Delete a specific message:


```
root@raspberrypi:/usr/local/bin# smsmanager delete 1
Message at index 1 deleted successfully
```

Delete all messages:

```
root@raspberrypi:/usr/local/bin#  smsmanager delete all
All messages deleted successfully
```

### Using a different modem port or baud rate

Command:
```
smsmanager --port /dev/ttyUSB0 --baudrate 9600 check
```

## Quiet Mode Output

When using the `-q` or `--quiet` option with the `check` command, the output will be formatted as shown in the "Checking received messages" section above. This format makes it easy to parse the output and use it in other scripts or programs.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is open source and available under the [MIT License](LICENSE).

## Acknowledgments

- Thanks to the pyserial library for making serial communication easy in Python.
- Inspired by the need for a simple, scriptable interface to GSM modems.
