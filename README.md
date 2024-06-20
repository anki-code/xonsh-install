<p align="center">
Best way to install xonsh on macOS or Linux and using it as core shell.
</p>

<p align="center">  
If you like the idea click ⭐ on the repo and <a href="https://twitter.com/intent/tweet?text=Nice%20xontrib%20for%20the%20xonsh%20shell!&url=https://github.com/anki-code/xonsh-install" target="_blank">tweet</a>.
</p>

## Motivation

Xonsh is a Python-based shell, and to run xonsh you must have Python installed. The Python version and its packages can be installed and located anywhere and when you execute `import` or any other Python code during a xonsh session, it will be executed in the Python environment that was used to run the current instance of xonsh. You must have good knowledge of this process after reading [xonsh-cheatsheet](https://github.com/anki-code/xonsh-cheatsheet/).

When xonsh becomes a core shell it's needed to keep python environment with xonsh stable, predictable and independent of any changes in the system. The lightweight environment managers like `venv`, `pipx` or `rye` will not help with this and it's needed to use package managers that have ability to install isolated python invironment as core feature e.g. `miniconda`, `micromamba`.

## mamba-install-xonsh

The `mamba-install-xonsh.sh` script creates independent python environment for xonsh using [mamba](https://mamba.readthedocs.io/). It's isolated xonsh-specific environment that can't be affected by upgrading the system packages, python version and other experiments around environments. You can use `xpip` and `xmamba` to install packages into this environment intentionally.

**Install stable**: the latest xonsh release with mostly tested python version:

```xsh
TARGET_DIR=$HOME/.local/xonsh-env PYTHON_VER=3.11 XONSH_VER='xonsh[full]>=0.17.0' \
 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/anki-code/xonsh-install/main/mamba-install-xonsh.sh)"
```

**Install the front line**: xonsh from main git branch with latest python version (known issues: [#5166](https://github.com/xonsh/xonsh/issues/5166)):

```xsh
TARGET_DIR=$HOME/.local/xonsh-env PYTHON_VER=3.12 XONSH_VER='git+https://github.com/xonsh/xonsh#egg=xonsh[full]' \
 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/anki-code/xonsh-install/main/mamba-install-xonsh.sh)"
```

**Install with stuff**: preinstall and preload xontribs (good for ssh and as manual alternative to [xxh](https://github.com/xxh/xxh)):

```xsh
TARGET_DIR=$HOME/.local/xonsh-env PYTHON_VER=3.11 XONSH_VER='git+https://github.com/xonsh/xonsh#egg=xonsh[full]' \
 XONTRIBS="xontrib-sh xontrib-jump-to-dir xontrib-pipeliner xontrib-prompt-bar xontrib-whole-word-jumping" \
 XONSHRC="xontrib load sh jump_to_dir pipeliner prompt_bar whole_word_jumping" \
 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/anki-code/xonsh-install/main/mamba-install-xonsh.sh)"
```

### Usage

Now forget about the cases where manipulations around python and packages break the shell unintended. Use `pip`, `brew` and other package managers without corrupting xonsh-env.

After installation:
* `xonsh` refers to `~/.local/xonsh-env/xbin/xonsh`.
* `xpip` refers to `~/.local/xonsh-env/bin/python -m pip`.

Additions:

* `xbin-xonsh` is to run xonsh from xonsh-env if xonsh overwritten by `$PATH`.
* `xbin-python` is to run python from xonsh-env.
* Use executable script from xonsh-env:
  * `xbin-hidden` is to list xonsh-env internal hidden `bin` directory. E.g. `xpip install lolcat && xbin-hidden # lolcat`.
  * `xbin-add` is to add executer from hidden `bin` to visible `xbin`. E.g. `xbin-add lolcat`.
  * `xbin-list` is to list visible `xbin` directory. E.g. `xbin-list # lolcat`.
  * `xbin-del` is to delete executer from `xbin`. E.g. `xbin-del lolcat`. It will stay in `bin`.

Note:

We do not recommend to use xonsh as a default login shell if you are not feel you strong and experienced. Because of most tools are waiting that login shell is POSIX-compliant you can face with issues when some tool is trying to run sh commands in xonsh.

### Tips and tricks

#### Using mamba from xonsh-env

To bind xonsh-env micromamba to `xmamba` alias run:
```xsh
source xmamba
```
Now you can:
```xsh
xmamba activate base
pip install lolcat  # Install `lolcat` into `base` env (where xonsh installed).
xmamba deactivate

xmamba create --name myenv python=3.12
xmamba activate myenv
pip install lolcat  # Install `lolcat` into `myenv`.
xmamba deactivate
```

#### Cleaning

If you have no plans to use `xmamba` [clean](https://fig.io/manual/mamba/clean) the disk space: `xmamba clean -a`.

## Another way to install xonsh

If you know how to install xonsh using another package manager - PR is welcome!

## See also
* [xonsh-cheatsheet](https://github.com/anki-code/xonsh-cheatsheet/tree/main) - Cheat sheet for xonsh shell with copy-pastable examples. The best doc for the new users. 
* [xonsh.AppImage](https://xon.sh/appimage.html) - one executable file which contains both xonsh and Python. AppImage allows xonsh to be run on any AppImage supported Linux distribution without installation or root access.
