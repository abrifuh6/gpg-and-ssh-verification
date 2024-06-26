# Creating and Configuring GPG Keys with GitHub

## Creating GPG Keys:

1. **Generate GPG Key Pair:**
   - Open your terminal.
   - Run the following command to generate a new GPG key pair:

     ```bash
     gpg --full-generate-key
     ```

   - Follow the prompts and choose the following options:

     - **Key Type:** RSA (default)
     - **Key Size:** 4096 bits (recommended for enhanced security)
     - **Expiration Period:** Choose an expiration period in days, weeks, months, or years. Alternatively, choose "0" for no expiration.
     - **Email Address:** Provide the email address associated with your GitHub account or the one you intend to use for signing commits.
     - **Passphrase (Optional):** You may be prompted to set a passphrase to protect your private key. Setting a passphrase is strongly recommended for enhanced security.

2. **List GPG Keys:**
   - After generating the key pair, list your GPG keys to obtain the key ID.
   - Run the following command:

     ```bash
     gpg --list-secret-keys --keyid-format LONG
     ```

   - Note down the key ID associated with the GPG key you want to use.

3. **Export Public Key:**
   - Export the public key associated with your GPG key pair.
   - Run the following command, replacing `<keyid>` with your keyid:

     ```bash
     gpg --armor --export <keyid>
     ```

   - Copy the output of this command; you'll need it to add your GPG key to GitHub.

## Adding GPG Key to GitHub:

1. **Log in to GitHub:**
   - Log in to your GitHub account.

2. **Access GPG Keys Settings:**
   - Go to "Settings" from the dropdown menu under your profile picture.

3. **Navigate to GPG Keys:**
   - In the settings sidebar, click on "SSH and GPG keys".

4. **Add GPG Key:**
   - Click on "New GPG key" or "Add GPG key".
   - Paste the public key you copied earlier into the provided text box.
   - Click "Add GPG key".

## Configuring Git to Use GPG Key:

1. **Associate GPG Key with Git:**
   - Once your GPG key is added to GitHub, configure Git to use it for signing commits.
   - Run the following commands, replacing `<your-gpg-key-id>` with the key ID you noted earlier:

     ```bash
     git config --global user.signingkey <your-gpg-key-id>
     git config --global commit.gpgsign true
     ```

   - These commands tell Git to use your GPG key for signing commits and set it as the default signing key.

2. **Verify Configuration:**
   - To verify that GPG signing is enabled, run:

     ```bash
     git config --get-all user.signingkey
     git config --get-all commit.gpgsign
     ```

   - Both commands should output the key ID and `true`, respectively.

### Adding GPG_TTY to Bash Environment:

1. **Open your Bash Configuration File:**
   - Open your `.bashrc` or `.bash_profile` file using a text editor. You can use `nano`, `vim`, or any other text editor of your choice. For example:

     ```bash
     nano ~/.bashrc
     ```

2. **Add Command to the File:**
   - Scroll to the bottom of the file and add the following line:

     ```bash
     export GPG_TTY=$(tty)
     ```

3. **Save and Close the File:**
   - Save the file and exit the text editor. If you're using `nano`, press `Ctrl + O` to save and `Ctrl + X` to exit.

4. **Source the File:**
   - After saving the changes, either restart your terminal session or run:

     ```bash
     source ~/.bashrc
     ```

   - This ensures that the changes take effect in your current terminal session.

---

### README: Creating and Configuring SSH Keys with GitHub

#### Generating SSH Keys:

1. **Generate SSH Key Pair:**
   - Open your terminal.
   - Run the following command to generate a new SSH key pair:

     ```bash
     ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
     ```

   - Replace `"your-email@example.com"` with your email address.
   - Optionally, you can specify a different file location and passphrase.

2. **Add SSH Key to SSH Agent:**
   - Start the SSH agent:

     ```bash
     eval "$(ssh-agent -s)"
     ```

   - Add your SSH private key to the SSH agent:

     ```bash
     ssh-add ~/.ssh/id_rsa
     ```

#### Adding SSH Key to GitHub:

1. **Log in to GitHub:**
   - Log in to your GitHub account.

2. **Access SSH Keys Settings:**
   - Go to "Settings" from the dropdown menu under your profile picture.

3. **Navigate to SSH Keys:**
   - In the settings sidebar, click on "SSH and GPG keys".

4. **Add SSH Key:**
   - Click on "New SSH key" or "Add SSH key".
   - Give your SSH key a title.
   - Paste the contents of your SSH public key (`~/.ssh/id_rsa.pub`) into the "Key" field.
   - Click "Add SSH key".

#### Testing SSH Connection:

1. **Test SSH Connection:**
   - Run the following command to test your SSH connection to GitHub:

     ```bash
     ssh -T git@github.com
     ```

   - You should see a message confirming your successful authentication.

2. **Confirm Host Fingerprint:**
   - Upon the first connection, you'll be asked to confirm the authenticity of the host by verifying its fingerprint.
   - Compare the fingerprint shown with GitHub's known fingerprints listed on their website.

---

These READMEs provide step-by-step instructions on creating and configuring GPG keys and SSH keys for use with GitHub. Follow these instructions to securely authenticate and interact with GitHub repositories using either GPG or SSH keys.