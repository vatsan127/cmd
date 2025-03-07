
## 1. User & Authentication
```sh
whoami                 # Show current user
useradd <username>     # Add a new user
su <username>          # Switch user
sudo passwd <username> # Set password for a user
```

## 2. File & Directory Management
```sh
ls -a                            # View hidden files
touch <file-name>{1..10}         # Create multiple files
touch -d tomorrow <file-name>    # Create a file with a future date
echo "<Message>" > <file-name>   # Write message to a file
```

## 3. File Compression
```sh
zip <zip-filename>.zip <filename>   # Compress a file
unzip <zip-filename>.zip            # Extract a zip file
```

## 4. File Viewing
```sh
less <file-name>   # View file content
head <file-name>   # View first 10 lines
tail <file-name>   # View last 10 lines
```

## 5. File Comparison
```sh
cmp <file1> <file2>  # Compare two files byte by byte
diff <file1> <file2> # Show differences between files
```

## 6. Sorting & Searching
```sh
cat <file> | sort                    # Sort file contents
find <path-to-check> -name <file-name> # Find file by name
find . -type f -name ".*"            # Find hidden files
find . -type f -empty                # Find empty files
find . -perm /a=x                    # Find executable files
```

## 7. File Permissions & Ownership
```sh
chmod +x <file>     # Make file executable
chown user file     # Change file ownership
```

## 8. Network & Connectivity
```sh
ifconfig               # Show network interface details
ip address             # Display IP address details
ping <site>            # Ping a website
ping -c <count> <site> # Limit ping count
netstat                # Show network connections
netstat -tulpan        # Show active connections with process details
```

## 9. System Information
```sh
uname          # Show system information
uname -a       # Show detailed system information
neofetch       # Display system info with graphics
cal            # Display calendar
free           # Show memory usage
df -H          # Show disk usage
```

## 10. Process Management
```sh
ps -aux            # Show running processes
top                # Display real-time process usage
htop               # Interactive process viewer
kill <PID>         # Kill a process by PID
pkill <process>    # Kill a process by name

systemctl stop <service>    # Stop a system service
systemctl start <service>   # Start a system service
systemctl restart <service> # Restart a system service

systemctl status <service>  # Show status of a service

systemctl enable <service>  # Enable a service to start on boot
systemctl disable <service> # Disable a service from starting on boot
```

## 11. Command History & Documentation
```sh
history    # Show command history
whatis <command>   # Show command description
whereis <command>  # Show command location
which <command>    # Show executable path of a command
```

