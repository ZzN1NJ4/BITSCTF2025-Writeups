# Appreciation Of Art

We were given a binary `a.art` and on running it we see this <br>
![image](https://github.com/user-attachments/assets/f9af8d21-6431-4345-b483-065709f60029)
<br>
Once again, This was something that I didn't exactly "reversed" and took a shortcut lol, but first comes some initial analysis I did. <br>

![image](https://github.com/user-attachments/assets/5aa50ed3-f1b4-4caa-b644-43619cec6a98)
![image](https://github.com/user-attachments/assets/60c7e670-0263-426c-963b-2935f9086f84)
![image](https://github.com/user-attachments/assets/9a97e023-fccb-4e18-83b2-955f214f09b3)
<br>
So It's a stripped binary, x64 and my guess for the reason behind those single char write calls is that they really didn't wanted us to look into any strings inside the binary.
Running strings didn't seem to be of much help as well. <br>
I did try r2 to reverse it but then quickly decided to take a simpler approach. I run the program again and then crash it using gcore to get the core dump and grep for strings in it. First we need to enable the core dump.

```bash
ulimit -c  # if 0 , then it's disabled
ulimit -c unlimited  # Now we can have core dump of any size
./a.art
ps aux | grep a.art
gcore -o dump <pid>
```
![image](https://github.com/user-attachments/assets/46ee2f7a-a93d-459c-b2bb-849af67ca8a8)

Although I couldn't see the name of the character, I did managed to get the flag.

![image](https://github.com/user-attachments/assets/23f9945d-08ce-4ba4-a5e5-e30b950a36f3)

### Flag
`BITSCTF{1_l0v3_0bfu5c4t1ng_thi1ng5_r4nd0mly_0e54826a}`
