## Dogen Initiallization

Dogen is the lab's local computer server (130.64.46.214)

1. Generate an SSH key pair for dogen and confirm they were both generated
```
	ssh-keygen -t ed25519 -f ~/.ssh/dogen-key -N ""
	ls ~/.ssh
```

The '-t ed25519' is the type of key that is being generated, and the '-N ""' sets the password to having no password needed to access the keys.

You should see a pair: dogen-key (private) and dogen-key.pub (public and safe to share). 

2. Send your public key to Kevin via Zulip via
	```cat ~/.ssh/dogen-key.pub```

3. Creating a config for Dogen
	```nano ~/.ssh/config```

	Add the following code within the nano, replacing 'User' (both places) with your username on dogen:
```
Host dogen  
HostName 130.64.46.214  
User (User)
IdentityFile ~/.ssh/dogen-key
```
Save and exit nano with Ctrl+O, Enter, then Ctrl+X.

4. Connect to dogen, and make sure you are on Tufts Secure network

```ssh dogen```

5.  Copy files between dogen and your laptop.
```
scp dogen:/[path_on_dogen] ~/[projects_folder]/
```
