# GUNHEAD (Very easy)

**Note for readers: I did not solve this challenge during the CTF as it was solved by my teammate.**

- The Docker container is spawned, and we are presented with a layout of the Gunhead AI bot.
- We also see the command line tool for the Gunhead AI, which should instantly make you think of the OS command injection vulnerability.

![1](https://github.com/vuld0/ca23-writeups/blob/main/Gunhead/1.png)  

- The ping command works perfectly fine, and you can also see the mechanism of its model function in the code:

```js
public function getOutput()
    {
        # Do I need to sanitize user input before passing it to shell_exec?
        return shell_exec('ping -c 3 '.$this->ip);
    }
```

- We tried to add a command with the ping command and guess what? it got executed - ``/ping google.com; id``

- However, we didn't find the flag in the present working directory (PWD), as it was present in the parent's parent directory.

```/ping  google.com; cat ../../flag.txt```

![2](https://github.com/vuld0/ca23-writeups/blob/main/Gunhead/2.png) 

- You can check the flag in the flag.txt file.
