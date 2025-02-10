# Loginator.out

For this one, we had given a file loginator.out and a series of hex strings. On running the binary, we see that it encodes the string in hex and prints it back. <br>

![Loginator](https://github.com/user-attachments/assets/755492ae-f513-45de-b1f3-e47d99a0ecd3)

Running this binary, We see this obfuscates the strings given to it

![image](https://github.com/user-attachments/assets/e8c90dea-ca67-4aaa-948e-aa6fbe75f8e9)

So this is the target hex 
> 02 92 a8 06 77 a8 32 3f 15 68 c9 77 de 86 99 7d 08 60 8e 64 77 be ba 74 26 96 e7 4e
<br>
with some guess work, I could make out a few initial characters and quickly wrote a python script to brute force all the others. Although I could "reverse" the binary and find out how it worked, this was way easier. <br> 

![image](https://github.com/user-attachments/assets/e50ec81f-f131-417c-ab3c-e5306f8d780a)


I automate the guess work in python until I find the matching hex and continue until I get to the end of the flag <br>

```python
import subprocess
import string

target = bytes.fromhex("02 92 a8 06 77 a8 32 3f 15 68 c9 77 de 86 99 7d 08 60 8e 64 77 be ba 74 26 96 e7 4e".replace("" , ""))

flag = "BITSCTF{"
possible="0123456789ABCDEFabcdef"

while "}" not in flag:
    for char in string.printable:
        attempt = flag + char
        result = subprocess.run(["./loginator.out", attempt], capture_output=True, text=True)
        output = result.stdout.strip()

        b_output = bytes.fromhex(output.replace(" ", "")) if all(c in "0123456789abcdefABCDEF " for c in output) else None
        if b_output and b_output.startswith(target[:len(b_output)]):  
            flag += char
            print(f"Flag: {flag}")
            break
```
<br>

![image](https://github.com/user-attachments/assets/e84e1f09-0cfb-4031-b8ad-9c70c332d443)
<br>

### Flag
`BITSCTF{C4ND4C3_L0G1C_W0RK?}`
