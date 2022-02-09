# DVGC20 VT22 Lab 1: Using Public Keys
## Assignment completion, in steps:
### Part 1: Encrypted file
1. Install [age](https://github.com/FiloSottile/age) `sudo apt install age -y` (only for Debian). Or [rage](https://github.com/str4d/rage).
2. Create plaintext file `vim foo.bar`, with text `Hello World!`.
3. Create private key `age-keygen -o oscar-private-key.txt`, output is: `Public key: age1jvsjvtjyzx4mty3nqcqfaedk93thryp4kgyms99scx7w59ktsy5qu4gr72` (the private key is `AGE-SECRET-KEY-1TQQ4JX7GHHJJS2UQ6HKKS72LFU9NALP6MUNJDNGRXUGYHZJYVHNQWLCYUP`).
4. Encrypt with Mahdi's public key `age -r age195v6c8pkyt5erx5nl4malpuuec2gc8z3xewfkylvnan34g6q6u9sdzmckn -i oscar-private-key.txt -a -o mahdi.foo.bar -e foo.bar` to file _mahdi.foo.bar_.
5. Encrypt with Samuel's public key `age -r age1es0kgeef4gxutm0tu55a0lxp25gzflprr57va76wc83ez84d93asq35ug6 -i oscar-private-key.txt -a -o samuel.foo.bar -e foo.bar` to file _samuel.foo.bar_.
### Part 2: SSH Authentication
