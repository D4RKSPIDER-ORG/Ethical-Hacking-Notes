

#### What we found:

- Website was not letting us log in.
    
- Adding `~` at the end of the URL (example: `/index.php~`) showed a **backup file** (common trick with Emacs/Vim).
    
- Inside the backup file, we saw **PHP code** with logic that checks username and password.
    

#### PHP Code Logic:

php

CopyEdit

`if ($username == $password) {     echo "Success"; } else {     if (sha1($username) === sha1($password)) {         echo file_get_contents("../flag.txt");     } else {         echo "Success";     } }`

#### Goal:

Trigger this condition:

php

CopyEdit

`if (sha1($username) === sha1($password))`

So we get the flag.

#### Normal way:

- You could try a **SHA-1 collision**, but that's complex and slow.
    

#### Smart Trick (easy bypass):

- **Send the inputs as arrays**, like this:
    

pgsql

CopyEdit

`username[]=123&password[]=456`

- In PHP, using `$_POST['username']` when `username[]` is sent will give an **array**, not a string.
    
- PHP `sha1(array)` gives **null** and a warning, not an error (in PHP 7).
    
- So now:
    

php

CopyEdit

`sha1($username) === sha1($password) null === null → true`

- This bypasses the check **without real SHA-1 collision**.
    

#### Result:

Server runs:

php

CopyEdit

`echo file_get_contents("../flag.txt");`

And you get the flag.

---

Let me know if you want this saved as a Markdown or text file.