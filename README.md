# mac-dev-playbook

This playbook installs the tools and configuration that I use on my Mac development machine,
via Ansible. Not everything on Mac OS can be automated so there are manual steps that must be
followed to set up this environment. However, the Ansible playbook bears the majority of the
responsibility.

There are a number of approaches can be taken to run this playbook. As always, it's best to use
tool versions that we know will work, so that this configuration is as reproducible as
possible. However, that requires installing some Python tooling, which isn't realistic on a
brand spankin new Mac computer.

Therefore, this README provides the following two installation methods:

- Local Installation (from the target Mac to the target Mac)
- Remote Installation (from another Mac computer to the target Mac, via SSH)

## Local installation

1. Ensure Apple's command line tools are installed by running the following command in the
   terminal:

    ```bash
    $ xcode-select -install
    ```

2. Add Python 3 to your `$PATH`:

    ```bash
    $ export PATH="$HOME/Library/Python/3.8/bin:/opt/homebrew/bin:$PATH"
    ```

3. Upgrade Pip:

    ```bash
    sudo pip3 install --upgrade pip
    ```

4. Install Ansible: 

    ```bash
    $ pip3 install ansible
    ```

5. Clone this repository to your local drive:

    ```bash
    $ git clone https://github.com/webdavis/mac-dev-playbook.git
    ```

6. Download the required Ansible roles:

    ```bash
    $ ansible-galaxy install -r requirements.yml
    ```

7. Open the App Store and **sign-in using your Apple ID** email, password, and Two-Factor
   Authentication (if it's turned on).

8. Run the playbook, entering your Mac OS account password when prompted for the `BECOME` password.

    ```bash
    $ ansible-playbook main.yml --ask-become-pass
    ```

## Remote installation

If this is your first time setting up the development environment for this project, then follow
the instructions in [mac-dev-environment.md](./docs/mac-dev-environment.md), instead. The
following instructions will assume that you've already done this and that you are returning to
work on this project.

### Setup SSH

(On the Mac you want to connect to) Run the following command:

```bash
$ sudo systemsetup -setremotelogin on
```

Edit the [`hosts.ini`](./hosts.ini) file and add the following line under `[remote]`:

```bash
[ip address or hostname of target mac] ansible_user=[mac ssh username]
```

If you need to supply an SSH password (if you don't use SSH keys), make sure to pass the
`--ask-pass` flag to the `ansible-playbook` command.

### pyevn

It's recommended to use pyenv to manage your Python version for this project.

Run the following command to instruct pyenv to switch to the version of Python tracked in the
[`.python-version`](./.python-version) file that lives in the root of this project:

```bash
$ eval "$(pyenv init -)"
```

> **Note:** this can be run from any folder in this project. **Additionally:** this command
> will need to be run every time you open a new terminal to work on this project.

### Poetry

Install Ansible and its dependencies with [Poetry](https://python-poetry.org/):

```bash
$ poetry install
```

### Enter the Python environment

**Note**: this will need to be done on every new shell.

```bash
$ poetry shell
```

## Running the playbook locally

```bash
$ ansible-playbook main.yml --ask-become-pass
```

## Running the playbook remotely

```bash
$ ansible-playbook main.yml --limit remote
```

> Remember when running remotely, if you need to supply an SSH password (if you don't use SSH
> keys), make sure to pass the `--ask-pass` flag to the `ansible-playbook` command.

### Running a specific set of tagged tasks

You can filter which part of the playbook to run by specifying a set of tags like so:

```bash
$ ansible-playbook main.yml -K --tags "mas,xcode"
```
