# Minimal set up for working SSH Git keychain in Windows

### 1.) Have a valid rsa public private key pair located in $HOME/.ssh
```notepad
id_rsa
id_rsa.pub
```

### 2.) Have Putty and its tools installed

Eg. installed in C:\Program Files\PuTTY and with the following tools:
```notepad
puttygen.exe
plink.exe
pageant.exe
```

### 3.) Create a ppk version of the public private key pair with puttygen
Open up puttygen, import the key, save as a ppk version in $HOME/.ssh

eg. we now have
```notepad
id_rsa
id_rsa.pub
id_rsa.ppk
id_rsa.pub.ppk
```

inside our .ssh directory

### Optional.) Create a Gitlab reference config for the Git environment you you have other public private keypairs

Inside .ssh dir create a file named config with the content
```notepad
Host gitlab.com
  HostName gitlab.com
  Preferredauthentications publickey
  IdentityFile ~/.ssh/id_rsa_otherkey
```

### 4.) Register the public key on Gitlab

### 5. Register the public key in plink, use powershell
```powershell
& 'C:\Program Files\PuTTY\plink.exe' git@gitlab.com
```

### 6.) Create an environment variable named GIT_SSH, and reference to plink
```notepad
GIT_SSH = C:\Program Files\PuTTY\plink.exe
```

### 7a.) Create a startup shortcut in the user local "Startup" directory for automating import
(It is ofc possible to create a task or a service also, but it is a bit overkill for this purpose)

Navigate to Startup
```notepad
C:\Users\$USER\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\peagant.lnk"
```

Create a shortcut that points to peagant.exe followed by all the public keys that we want to load automaticly when windows start.

Target
```notepad
"C:\Program Files\PuTTY\pageant.exe" C:\Users\$HOME\.ssh\id_rsa.ppk
```

### 7b.) Screw the the "Startup" location and create the shortcut anywhere you like for manual imports of private keys.


### 9.) Try pull and push something
```bash

```