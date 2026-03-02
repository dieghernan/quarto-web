# Tarball Installation On Linux

[\_](_ "Download Quarto") Find your operating system in the table below

You can install Quarto for a single user on Linux by using the Quarto tarball and following the below set of steps.

**1. Download the tarball**

``` bash
wget https://github.com/quarto-dev/quarto-cli/releases/download/v^version^/quarto-^version^-linux-amd64.tar.gz
```

**2. Extract Files**

Extract the contents of the tarball to the location where you typically install software (e.g. `~/opt`). For example:

``` bash
mkdir ~/opt
tar -C ~/opt -xvzf quarto-^version^-linux-amd64.tar.gz
```

**3. Create a Symlink**

Create a symlink to `bin/quarto` in a folder that is in your path. If there is no such folder, you can create a folder such as `~/.local/bin` and place the symlink there. For example:

For example:

``` bash
mkdir ~/.local/bin
ln -s ~/opt/quarto-^version^/bin/quarto ~/.local/bin/quarto
```

**4. Ensure Folder in on Path**

If you can run `quarto -v` at this point, jump ahead to the next step.

Otherwise, ensure that the folder where you created a symlink is in the path. For example:

``` bash
( echo ""; echo 'export PATH=$PATH:~/.local/bin\n' ; echo "" ) >> ~/.profile
source ~/.profile
```

**5. Check The Installation**

Use `quarto check` to confirm that the installation is successful:

``` bash
quarto check
```
