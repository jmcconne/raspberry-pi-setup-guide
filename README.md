# Raspberry Pi Setup Guide

This guide will walk you through setting up your Raspberry Pi with pyenv for managing Python versions and Docker for creating images and running containers.

## Prerequisites

- A Raspberry Pi with Raspberry Pi OS (64-bit) installed
- Internet connection
- Terminal access

## Installing pyenv

pyenv is a tool that allows you to easily switch between multiple versions of Python. Follow these steps to install pyenv on your Raspberry Pi:

1. **Update and install dependencies:**

    ```sh
    sudo apt update
    sudo apt install build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev curl git \
    libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
    ```

2. **Install pyenv:**

    ```sh
    curl https://pyenv.run | bash
    ```

3. **Add pyenv to your shell startup scripts:**

    Add the following lines to your `~/.bashrc` file:

    ```sh
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
    echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(pyenv init - bash)"' >> ~/.bashrc
    ```

    Then, if you have `~/.profile`, `~/.bash_profile` or `~/.bash_login`, add the commands there as well. If you have none of these, create a `~/.profile` and add the commands there.

    * To add to `~/.profile`:
       ``` bash
       echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
       echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
       echo 'eval "$(pyenv init - bash)"' >> ~/.profile
       ```
     * To add to `~/.bash_profile`:
       ```bash
       echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
       echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
       echo 'eval "$(pyenv init - bash)"' >> ~/.bash_profile
       ```
    * To add to `~/.bash_login`:
       ```bash
       echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_login
       echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_login
       echo 'eval "$(pyenv init - bash)"' >> ~/.bash_login
       ```

4. **Restart your shell:**

    ```sh
    exec "$SHELL"
    ```

## Setting the Global Python Version using pyenv

Replace `3.12.9` below with another version of Python if you prefer.

1. **Install a Python version:**

    ```sh
    pyenv install 3.12.9
    ```

2. **Set the global Python version:**

    ```sh
    pyenv global 3.12.9
    ```

3. **Verify the installation:**

    ```sh
    python --version
    ```

    This should output `3.12.9` or whichever Python version you specified.

## Installing Docker

Docker is a platform for developing, shipping, and running applications in containers. Follow these steps to install Docker on your Raspberry Pi:

1. **Update and install dependencies:**

    ```sh
    sudo apt update
    sudo apt install ca-certificates curl
    ```

2. **Add Docker’s official GPG key:**

    ```sh
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    ```

3. **Set up the stable repository:**

    ```sh
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt update
    ```

4. **Install Docker Engine:**

    ```sh
    sudo apt update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

5. **Verify Docker installation:**

    ```sh
    sudo docker run hello-world
    ```

    This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

6. **Manage Docker as a non-root user:**

    ```sh
    sudo usermod -aG docker $USER
    ```

    Log out and log back in so that your group membership is re-evaluated.

## Conclusion

You have successfully set up pyenv and Docker on your Raspberry Pi. You can now manage multiple Python versions and create and run Docker containers.

For more information, refer to the official documentation of [pyenv](https://github.com/pyenv/pyenv) and [Docker](https://docs.docker.com/get-started/).
