# ssh

This document describes how to generate SSH keys and add them to `ssh-agent`.

The content in this file comes from two main sources.
- [Github doc](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [FOSS Linux](https://www.fosslinux.com/122405/how-to-install-and-use-ssh-agent-on-ubuntu.htm)

## Generating a new SSH key

1. Open a terminal.

2. Paste the text below, replacing the email used in the example with your email address.

    ```sh
    ssh-keygen -t ed25519 -C "your.email@example.com"
    ```

    This creates a new SSH key, using the provided email as a label.

    ```
    > Generating public/private ALGORITHM key pair.
    ```

    When you're prompted to "Enter a file in which to save the key", you can press Enter to accept the default file location.
    Please note that if you created SSH keys previously, ssh-keygen may ask you to rewrite another key, in which case we
    recommend creating a custom-named SSH key. To do so, type the default file location and replace `id_ALGORITHM` with your
    custom key name.

    ```
    > Enter a file in which to save the key (/home/YOU/.ssh/ALGORITHM):[Press enter]
    ```

    At the prompt, type a secure passphrase.

    ```
    > Enter passphrase (empty for no passphrase): [Type a passphrase]
    > Enter same passphrase again: [Type passphrase again]
    ```

## Adding your SSH key to the ssh-agent

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated
a new SSH key. 

1. Start the ssh-agent in the background.

  ```sh
  $ eval "$(ssh-agent -s)"
  > Agent pid 5954
  ```

2. Add your SSH private key to the ssh-agent.

    If you created your key with a different name, or if you are adding an existing key that has a different name, replace `id_ed25519` in the command with the name of your private key file.

    ```sh
    ssh-add ~/.ssh/id_ed25519
    ```

## Auto-start ssh-agent

To auto-start ssh-agent whenever you start a terminal, you can add the `eval "$(ssh-agent -s)"` command to your shell's
profile script.

For bash users, the file is `~/.bashrc`. For Zsh users, it is `~/.zshrc`.

```sh
echo 'eval "$(ssh-agent -s)"' >> ~/.bashrc
```

## Make ssh-agent automatically add the key on demand

SSH supports adding a key to the agent on first use (since version 7.2).

You can enable that feature by putting the following into `~/.ssh/config`:

```
AddKeysToAgent confirm
```

This also works when using derivative tools, such as git.

From the From the [7.2 changelog](https://www.openssh.com/txt/release-7.2):

```
ssh(1): Add an AddKeysToAgent client option which can be set to 'yes', 'no', 'ask', or 'confirm', and defaults to 'no'.
When enabled, a private key that is used during authentication will be added to ssh-agent if it is running (with confirmation enabled if set to 'confirm').
```

## List keys added to ssh-agent

```sh
ssh-add -l
```
