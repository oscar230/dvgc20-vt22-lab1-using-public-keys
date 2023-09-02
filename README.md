# DVGC20 VT22 Lab 1: Using Public Keys
## Part 1: Encrypted file
### Install
1. Install
    ```bash
    $ wget "https://github.com/str4d/rage/releases/download/v0.9.1/rage_0.9.1_amd64.deb"
    $ sudo apt install ./rage_0.9.1_amd64.deb -y
    ```
### Create keypair and encrypt
1. Create key-pair
    ```bash
    $ rage-keygen -o key.txt
    Public key: age1rjdtmp2f5zn3ljcd92cfajgtevwtvfnsmxvx7tqmy7lpftwfhs5qwz66rh
    ```
2. Create file and encrypt using Mahdi's key
    ```bash
    $ echo "test" > plaintext
    $ cat plaintext
    test
    $ cat plaintext | rage -r age195v6c8pkyt5erx5nl4malpuuec2gc8z3xewfkylvnan34g6q6u9sdzmckn > crypt.age
    ```
2. Send email to Mahdi and Samuel with the file *crypt.age* and with the text *only Mahdi can decrypt the attached file.*.

### Cleanup
1. Cleanup
   ```bash
   rm rage_0.9.1_amd64.deb plaintext* crypt.age
   sudo apt remove -y rage
   ```

## Part 2: SSH Authentication
1. Connect `ssh oscaande104@hex.cse.kau.se`, got fingerprint `ECDSA key fingerprint is SHA256:pB1lZf5IkBmBfLJXvuycTzHPhaFe6c87VOtsZg7Hl6Q` and selecting *yes* to trust this. Inputing KAUID password and being greeted with;
    ```bash
    Welcome to Ubuntu 18.04.6 LTS (GNU/Linux 4.15.0-208-generic x86_64)
    ...
    ```
2. The connection works, now `exit`.
3. Generate key
    ```bash
    oscar@DESKTOP-CCRNBR0:~$ ssh-keygen -t ed25519
    Generating public/private ed25519 key pair.
    ...
    The key's randomart image is:
    +--[ED25519 256]--+
    |EB.     ...      |
    |O+o.   .   .     |
    |+*O   .     o .  |
    |o*oO o     o + . |
    |+.o.*   S . * o  |
    | o...    . + . . |
    |  .o        . .  |
    |  o  o       o   |
    |   ++ .     .    |
    +----[SHA256]-----+
    ```
4. Login to the server again using password, and input ssh key fingerprint 
    ```
    ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJiu26bcFkazLEhtFaeGALRQNXLlhzRB5v0Cql5DAFU2 oscar@DESKTOP-CCRNBR0
    ```
    from `.ssh/id_ed25519.pub` from the client to `∼/.ssh/authorized_keys` on the server using vim.
5. `Exit` ssh session.
6. Login using `ssh oscaande104@hex.cse.kau.se -v` to see the debug log, the log says `debug1: Will attempt key: /home/oscar/.ssh/id_ed25519 ED25519 SHA256:d1YLzrcaFACqljDzDPqUwEGIrWZ0AKTg8+s3ugREvAE` and then `debug1: Server accepts key: /home/oscar/.ssh/id_ed25519 ED25519 SHA256:d1YLzrcaFACqljDzDPqUwEGIrWZ0AKTg8+s3ugREvAE` which results in `debug1: Authentication succeeded (publickey).`.
7. Cleanup `rm .ssh/id_ed25519*; truncate .ssh/known_hosts --size 0`