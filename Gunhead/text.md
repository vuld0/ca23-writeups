Here's the corrected markdown file with grammatical and technical errors fixed:

GUNHEAD
Note for readers: I did not solve this challenge during the CTF as it was solved by my teammate.

The Docker container is spawned, and we are presented with a layout of the Gunhead AI bot.
We also see the command line tool for the Gunhead AI, which should instantly make you think of the OS command injection vulnerability.
1
The ping command works perfectly fine, and you can also see the mechanism of its model function in the code:
js
Copy code
public function getOutput()
{ # Do I need to sanitize user input before passing it to shell_exec?
return shell_exec('ping -c 3 '.$this->ip);
}
We tried to add a command with the ping command, and it executed successfully: /ping google.com; id.

However, we didn't find the flag in the present working directory (PWD), as it was present in the parent's parent directory.

To fetch the flag, we used the following command: /ping google.com; cat ../../flag.txt.

You can check the flag in the flag.txt file.
