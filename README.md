# Mac Developer Machine Setup

This repository contains useful scripts to set up a mac development machine. They have been tested with the following OSes:

| OS                                                              | SKU     | Version(s)   |
| --------------------------------------------------------------- | ------- | ------------ |
| [macOS](https://www.apple.com/macos/)                           | Desktop | 10.15        |

## Pre-Requisites

### macOS

1. Install [Homebrew](https://docs.brew.sh/)
1. Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-macos)
1. Set up Python 3 as the default version of Python:

   ```bash
   echo "alias python='python3'" >> ~/.zshrc
   echo "export PATH=$HOME/Library/Python/3.7/bin:$PATH" >> ~/.zshrc
   ```

1. Add secretes

    ```bash
    echo "export GITHUB_NOTIFICATIONS_TOKEN=" >> ~/.zshenv
    echo "export ANSIBLE_PIANO_USER=" >> ~/.zshenv
    echo "export ANSIBLE_PIANO_PW=" >> ~/.zshenv
    ```

## Running

Before running the scripts, please review `_all.yaml` and `_all_no_customization.yaml`, and comment out software you don't want installed. In particular, most folders contain `customization.yaml` files which tend to contain my personal opinions on customizations; feel free to comment out sections of those files, or ignore them entirely.

To run the setup:

```bash
ansible-playbook -K _all.yaml
```

You will be prompted for your password, so that administrative-level software can be installed. _**You must be a sudoer to run these scripts, otherwise the installation process will fail.**_ You can also run individual files if you'd prefer to take more control over what's executed.

Since core OS packages are upgraded, it is safest to reboot the PC/VM after running these scripts. At a bare minimum, many UI shell customizations done here will require you to log out and log back in.

## After Running

1. Import all used gpg keys
   - `gpg --export-secret-keys "name of key" > private.key
   - `gpg import private.key`
