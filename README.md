# System-Administration-and-Scripting-Toolkit
1. System Information Script (Perl or Shell Scripting):
Perl Script:

```
#!/usr/bin/perl

print "Uptime:\n";
system('uptime');

print "\nFree Memory:\n";
system('free -h');

print "\nDisk Usage:\n";
system('df -h');

print "\nRunning Processes:\n";
system('ps aux | head');
```
Save the file as sys_info.pl and make it executable using chmod +x sys_info.pl.

2. Backup Script (Korn Shell or Bourne Shell):
```
#!/bin/ksh

SOURCE_DIR="/path/to/important/dir"
BACKUP_NAME="backup_$(date +%Y%m%d%H%M%S).tar.gz"
BUCKET_NAME="your-aws-s3-bucket-name"
LOG_FILE="/path/to/logfile.log"

tar -czvf $BACKUP_NAME $SOURCE_DIR 2>> $LOG_FILE
aws s3 cp $BACKUP_NAME s3://$BUCKET_NAME/ 2>> $LOG_FILE

echo "Backup completed on $(date)" >> $LOG_FILE
```
Save the file as backup.sh and make it executable using chmod +x backup.sh.

3. User Management Utility (Using C):
This is a more complex task. Here's a simplified version:
```    
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    if (argc < 3) {
        printf("Usage: %s <add/delete/modify> <username>\n", argv[0]);
        exit(1);
    }
    
    char *action = argv[1];
    char *username = argv[2];

    if (strcmp(action, "add") == 0) {
        system("useradd %s", username);
    } else if (strcmp(action, "delete") == 0) {
        system("userdel %s", username);
    } else if (strcmp(action, "modify") == 0) {
        // Implement modify logic (e.g., change password, change shell, etc.)
    } else {
        printf("Invalid action\n");
        exit(1);
    }

    return 0;
}
```
Compile the C code using gcc user_mgmt.c -o user_mgmt.

4. Performance Monitoring (Python):
```
import psutil
import boto3

# Thresholds
CPU_THRESHOLD = 80
MEMORY_THRESHOLD = 80

cpu_usage = psutil.cpu_percent()
memory_info = psutil.virtual_memory()

if cpu_usage > CPU_THRESHOLD:
    message = f"CPU usage exceeded: {cpu_usage}%"
    # Send to AWS SNS or email
    # boto3.client('sns').publish(TopicArn='your-topic-arn', Message=message)

if memory_info.percent > MEMORY_THRESHOLD:
    message = f"Memory usage exceeded: {memory_info.percent}%"
    # Send to AWS SNS or email
    # boto3.client('sns').publish(TopicArn='your-topic-arn', Message=message)
```
Similarly, you can add checks for disk I/O and other metrics.

Save the file as performance_monitor.py.
