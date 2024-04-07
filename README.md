<p align="center">
Best way to install xonsh on macOS or Linux and using it as core shell.
</p>

<p align="center">  
If you like the idea click ⭐ on the repo and <a href="https://twitter.com/intent/tweet?text=Nice%20xontrib%20for%20the%20xonsh%20shell!&url=https://github.com/anki-code/xonsh-install" target="_blank">tweet</a>.
</p>

## Motivation

Xonsh is a Python-based shell, and to run xonsh you must have Python installed. The Python version and its packages can be installed and located anywhere and when you execute `import` or any other Python code during a xonsh session, it will be executed in the Python environment that was used to run the current instance of xonsh. You must have good knowledge of this process after reading [xonsh-cheatsheet](https://github.com/anki-code/xonsh-cheatsheet/).

When xonsh becomes a core shell it's needed to keep python environment with xonsh stable, predictable and independent of any changes in the system.

The `mamba-install-xonsh.sh` script implements this by creating python environment for xonsh using mamba. It's isolated xonsh-specific environment that can't be affected by upgrading the system packages, python version and other experiments around environments. The xonsh shell will work as well as installing and updating the packages using `xpip` and `xmamba`.

## Install xonsh

Choose the `TARGET_DIR` and run installation:

```xsh
TARGET_DIR=$HOME/.local/xonsh-env PYTHON_VER=3.12 /bin/bash \
  -c "$(curl -fsSL https://raw.githubusercontent.com/anki-code/xonsh-install/main/mamba-install-xonsh.sh)"
# Restart session
```

Now you have:
```xsh
which xonsh
# /Users/user/.local/xonsh-env/xbin/xonsh  # You can run this directly from any place.
xonsh

which xpip
# /Users/user/.local/xonsh-env/bin/python -m pip
which xmamba
# /Users/user/.local/xonsh-env/xbin/xmamba
```

Now forget about the cases where manipulations around python and packages break the shell unintended.

## See also
* [xonsh-cheatsheet](https://github.com/anki-code/xonsh-cheatsheet/tree/main)
