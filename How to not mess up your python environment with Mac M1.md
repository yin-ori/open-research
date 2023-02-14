# How to not mess up your python environment with Mac M1

---
tested with: 
Macbook Air M1 Ventura
Brew 3.6.21
Pyenv pyenv 2.3.12-16-gc8daaa39
Python 3.11.1
---

## Wrong Python Package Path
* if pip environment is correct, but packages are installed to wrong location, check `pip config list`
	* if the target is wrong, search for the `pip.conf` file
* should be here `/Users/<myusername>/.config/pip/pip.conf`
* amend the path to the correct one
* check with `pip config list` if the changes were applied correctly
---
## Fresh Start
### Running Homebrew's uninstall script
* `$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"` or see [git docu](https://github.com/homebrew/install#uninstall-homebrew)
* `The following possible Homebrew files were not deleted [...]` --> delete manually or run `sudo rm -rf /opt/homebrew/`
### Remove Homebrew shell configuration
* run `cat ~/.zprofile`
* delete this line `eval "$(/opt/homebrew/bin/brew shellenv)"`
* check whether traces are still there with `ls -ag /opt` (total should be 0)
### Reinstall Homebrew 
* see & follow [git docu](https://docs.brew.sh/Installation) 
* if Homebrew asks you to add lines to your .zprofile through terminal command, do so!  (or add with `nano ~/.zprofile`)
### Install Pyenv through Github
* clone the pyenv repo into your home folder:
```
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
$ cd ~/.pyenv && src/configure && make -C src
```
* edit .zshrc and add the following lines at the bottom of the file 
```
export PYENV_ROOT="$HOME/.pyenv" 
export PATH="$PYENV_ROOT/bin:$PATH" 
eval "$(pyenv init --path)" 
eval "$(pyenv init -)"
```
* quit your terminal and reopen it
* pyenv should be activated and you can start to install some Python `pyenv install --list` --> `pyenv install <your preferred version>`
#### Test Environment 
* `pyenv shell <your preferred version>` 
* test `which pip` `pyenv -V`
