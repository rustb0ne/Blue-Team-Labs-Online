# Question 1) Is it an internal or external attack, what is the attacker IP?

To identify the attack source, we search for connection attempts using `grep` with the keyword `connection from`.

The output reveals an IP address starting with `192.168.x.x`, indicating this is an internal attack

![alt text](image.png)

# Question 2) How many valid accounts did the attacker find, and what are the usernames?

Searching for `user` in the text viewer reveals lines containing username information

![alt text](image-1.png)

Now we'll use `grep` combined with column extraction using `awk`, `sort`, and `uniq` to extract the usernames that were attempted during the brute force attack

![alt text](image-2.png)

For non-existent usernames, the log records them as `invalid`. We attempted to find lines without the `invalid` keyword, but this `grep` command proved ineffective

![alt text](image-3.png)

Instead, we search using the keyword `failed password` rather than `userauth` for better results.

![alt text](image-4.png)

# Question 3) How many times did the attacker login to these accounts?

We search for lines containing `sophia`

![alt text](image-5.png)

We filter out entries containing `debug`, `error`, and `failed` to focus on successful authentication attempts

![alt text](image-6.png)

Counting the number of `accepted` entries in the output gives us the final result

# Question 4) When was the first request from the attacker recorded?

By examining the earliest log entries from the attacker's IP address, we can identify the timestamp of the first connection attempt

![alt text](image-7.png)

# Question 5) What is the log level for the log file?

The log file contains numerous entries marked as `debug1`, `debug2`, and `debug3`, indicating that the log level is set to Debug

# Question 6) Where is the log file located in Windows?

Based on the OpenSSH architecture for Windows:

Configuration files and logs (equivalent to `/etc` and `/var/log` on Linux) are redirected to `C:\ProgramData\ssh\`

The default log filename follows the service name (sshd), resulting in `sshd.log`

Therefore, the log file path is: C:\ProgramData\ssh\logs\sshd.log
