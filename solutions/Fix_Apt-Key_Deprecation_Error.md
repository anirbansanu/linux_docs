It's important to handle deprecated apt-key warnings carefully to maintain system security. 

### Background
When managing packages on Ubuntu, `apt-key` is used to manage repositories' cryptographic keys that ensure package integrity and security. Over time, some methods used by `apt-key` have been deprecated in favor of newer, more secure practices.

### Problem
You encounter warnings about deprecated `apt-key` usage when running `sudo apt update`. These warnings indicate that certain repository keys are managed in a way that is no longer recommended due to security concerns.

### Solution: Method 1 (Recommended Approach)

#### Step 1: Identify the Deprecated Key

1. **List All Keys:**
   Open a terminal and run:
   ```bash
   sudo apt-key list
   ```
   This command lists all the keys currently installed on your system.

2. **Locate the Key:**
   Look through the list for the key associated with the package repository causing the warning. For example, if you see warnings related to TeamViewer, locate its key in the list.

#### Step 2: Export and Convert the Key

1. **Extract Key ID:**
   Identify the ID of the key you want to manage. This is typically the last 8 characters in the second line of the key listing, enclosed in square brackets, such as `[SC]`.

2. **Export the Key:**
   Use `apt-key export` followed by `gpg` to convert and save the key securely:
   ```bash
   sudo apt-key export 0C1289C0 | sudo gpg --dearmour -o /etc/apt/trusted.gpg.d/teamviewer.gpg
   ```
   Replace `0C1289C0` with the key ID you identified. This command exports the key and converts it into a `.gpg` file (`teamviewer.gpg` in this example) stored in `/etc/apt/trusted.gpg.d/`.

#### Step 3: Update and Verify

1. **Update APT:**
   After saving the key, update APT to verify the changes:
   ```bash
   sudo apt update
   ```
   Running `apt update` ensures that the repository no longer triggers the deprecated key warning.

### Method 2: Quick Fix (Not Recommended) *( This works for me )*

#### Step 1: Quick Copy Method

1. **Quick Copy:**
   If you prefer a quick but less secure solution:
   ```bash
   cd /etc/apt
   sudo cp trusted.gpg trusted.gpg.d
   ```
   This command duplicates `trusted.gpg` as `trusted.gpg.d`, which may suppress warnings related to legacy keys.

#### Step 2: Caution

1. **Security Implications:**
   This method is not recommended as it might compromise system security by circumventing key validation checks that ensure package authenticity.

### Conclusion

- **Security First:** Always prioritize security by using Method 1 to manage deprecated `apt-key` warnings.
- **System Maintenance:** Regularly update and manage repository keys to ensure the security and integrity of your system's package installations.
- **Best Practices:** Follow recommended practices from Ubuntu and other trusted sources to handle cryptographic keys effectively.

By following these steps, you can effectively manage and resolve `apt-key` deprecation warnings on your Ubuntu system while maintaining robust security practices.