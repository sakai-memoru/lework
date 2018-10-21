＞ [Home](../index.md)

# conda初歩

## Overview
- pythonのパッケージ管理、環境管理に使うcondaコマンドを説明する。

## Environment
- 事前に以下をインストール済みであること
  - anaconda
  - https://www.anaconda.com/
  - download
  - https://www.anaconda.com/download/
  - installation
  - https://conda.io/docs/user-guide/install/index.html

## Contents
### 1. Execute Anaconda Prompt
1. win key
2. input `anaconda prompt`
3. Enter

### 2. Conda Operation
- references
  - Condaの使い方メモ
  - https://qiita.com/showsuzu/items/e2fddf22f725f4d2ab8c

#### 2.0. operation `where conda`
```
(base) G:\Users\sakai>where conda
G:\Users\sakai\Anaconda3\Library\bin\conda.bat
G:\Users\sakai\Anaconda3\Scripts\conda.exe
```

#### 2.1. operation `conda --version`
```
(base) G:\Users\sakai>conda --version
conda 4.5.11
```

#### 2.2. operation `conda`
```
(base) G:\Users\sakai>conda
usage: conda [-h] [-V] command ...

conda is a tool for managing and deploying applications, environments and packages.

Options:

positional arguments:
  command
    clean        Remove unused packages and caches.
    config       Modify configuration values in .condarc. This is modeled
                 after the git config command. Writes to the user .condarc
                 file (G:\Users\sakai\.condarc) by default.
    create       Create a new conda environment from a list of specified
                 packages.
    help         Displays a list of available conda commands and their help
                 strings.
    info         Display information about current conda install.
    install      Installs a list of packages into a specified conda
                 environment.
    list         List linked packages in a conda environment.
    package      Low-level conda package utility. (EXPERIMENTAL)
    remove       Remove a list of packages from a specified conda environment.
    uninstall    Alias for conda remove. See conda remove --help.
    search       Search for packages and display associated information. The
                 input is a MatchSpec, a query language for conda packages.
                 See examples below.
    update       Updates conda packages to the latest compatible version. This
                 command accepts a list of package names and updates them to
                 the latest versions that are compatible with all other
                 packages in the environment. Conda attempts to install the
                 newest versions of the requested packages. To accomplish
                 this, it may update some packages that are already installed,
                 or install additional packages. To prevent existing packages
                 from updating, use the --no-update-deps option. This may
                 force conda to install older versions of the requested
                 packages, and it does not prevent additional dependency
                 packages from being installed. If you wish to skip dependency
                 checking altogether, use the '--force' option. This may
                 result in an environment with incompatible packages, so this
                 option must be used with great caution.
    upgrade      Alias for conda update. See conda update --help.

optional arguments:
  -h, --help     Show this help message and exit.
  -V, --version  Show the conda version number and exit.

conda commands available from other packages:
  build
  convert
  develop
  env
  index
  inspect
  metapackage
  render
  server
  skeleton
  verify
```

#### 2.3. operation `conda info -e`
```
(base) G:\Users\sakai>conda info -e
# conda environments:
#
base                  *  G:\Users\sakai\Anaconda3
fstep                    G:\Users\sakai\AppData\Local\conda\conda\envs\fstep

```

#### 2.4.  operation `conda create -n fenv python=3.7`

```
(base) G:\Users\sakai>conda create -n fenv python=3.7
Solving environment: done

## Package Plan ##

  environment location: G:\Users\sakai\Anaconda3\envs\fenv

  added / updated specs:
    - python=3.7


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    wheel-0.32.1               |           py37_0          52 KB
    setuptools-40.4.3          |           py37_0         576 KB
    certifi-2018.10.15         |           py37_0         138 KB
    pip-10.0.1                 |           py37_0         1.7 MB
    wincertstore-0.2           |           py37_0          13 KB
    python-3.7.0               |       hea74fb7_0        21.1 MB
    ------------------------------------------------------------
                                           Total:        23.6 MB

The following NEW packages will be INSTALLED:

    certifi:        2018.10.15-py37_0
    pip:            10.0.1-py37_0
    python:         3.7.0-hea74fb7_0
    setuptools:     40.4.3-py37_0
    vc:             14.1-h0510ff6_4
    vs2015_runtime: 14.15.26706-h3a45250_0
    wheel:          0.32.1-py37_0
    wincertstore:   0.2-py37_0

Proceed ([y]/n)? y
:
:
#
# To activate this environment, use
#
#     $ conda activate fenv
#
# To deactivate an active environment, use
#
#     $ conda deactivate


(base) G:\Users\sakai>conda info -e
# conda environments:
#
base                  *  G:\Users\sakai\Anaconda3
fenv                     G:\Users\sakai\Anaconda3\envs\fenv
fstep                    G:\Users\sakai\AppData\Local\conda\conda\envs\fstep
```

#### 2.5.  operation `conda activate fenv`

```
(base) G:\Users\sakai>conda activate fenv

(fenv) G:\Users\sakai>python --version
Python 3.7.0

(fenv) G:\Users\sakai>where python
G:\Users\sakai\Anaconda3\envs\fenv\python.exe
G:\Users\sakai\Anaconda3\python.exe
G:\Users\sakai\AppData\Local\Programs\Python\Python36-32\python.exe

(fenv) G:\Users\sakai>pip --version
pip 10.0.1 from G:\Users\sakai\Anaconda3\envs\fenv\lib\site-packages\pip (python 3.7)
(fenv) G:\Users\sakai>pip freeze
certifi==2018.10.15
wincertstore==0.2

(fenv) G:\Users\sakai>python
Python 3.7.0 (default, Jun 28 2018, 08:04:48) [MSC v.1912 64 bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> for p in sys.path:
...     print(p)
...

G:\Users\sakai\Anaconda3\envs\fenv\python37.zip
G:\Users\sakai\Anaconda3\envs\fenv\DLLs
G:\Users\sakai\Anaconda3\envs\fenv\lib
G:\Users\sakai\Anaconda3\envs\fenv
G:\Users\sakai\Anaconda3\envs\fenv\lib\site-packages
>>> quit()
```

#### 2.6.  operation `conda deactivate`
```
(fenv) G:\Users\sakai>conda deactivate

(base) G:\Users\sakai>
```

#### 2.7.  operation `conda remove fenv --all`
```
(base) G:\Users\sakai>conda remove -n fenv --all

Remove all packages in environment G:\Users\sakai\Anaconda3\envs\fenv:


## Package Plan ##

  environment location: G:\Users\sakai\Anaconda3\envs\fenv


The following packages will be REMOVED:

    certifi:        2018.10.15-py37_0
    pip:            10.0.1-py37_0
    python:         3.7.0-hea74fb7_0
    setuptools:     40.4.3-py37_0
    vc:             14.1-h0510ff6_4
    vs2015_runtime: 14.15.26706-h3a45250_0
    wheel:          0.32.1-py37_0
    wincertstore:   0.2-py37_0

Proceed ([y]/n)? y


(base) G:\Users\sakai>conda info -e
# conda environments:
#
base                  *  G:\Users\sakai\Anaconda3
fstep                    G:\Users\sakai\AppData\Local\conda\conda\envs\fstep
```
## Wrapup
- pythonのパッケージ管理、環境管理に使う主なcondaコマンドを説明した。

|command|function|
|-------|--------|
|`conda info -e`|管理しているpython環境の一覧表示|
|`conda create -n <env name> python=3.7`|pythonのバージョンを指定してのpython環境生成|
|`conda activate <env name>`|対象環境のアクティベート|
|`conda deactivate`|対象環境のデアクティベート|
|`conda remove -n <env name> --all`|対象環境の完全削除|

[EOF]
