# 1805-python-environment-first-step


##  Overview

- python��virtualenv on windows�̃C���X�g�[���ƁA���\�z�ɂ��āA�L�q����B


##  1. python installation

- python �T�C�g�ɂāApython���_�E�����[�h���āA�C���X�g�[������B
  + https://www.python.org/
- reference
  �{ Python���C���X�g�[������ifor Windows�j
�@�@�@* https://qiita.com/taiponrock/items/f574dd2cddf8851fb02c

- ���ϐ� path�ɁApython�̃p�X��ǉ�����B

- �ȉ��Apowershell�Ŋm�F�B

``` powershell
PS > $Env:path.split(";") | out-string -stream | sls py

G:\Users\<username>\AppData\Local\Programs\Python\Python36-32\Scripts\
G:\Users\<username>\AppData\Local\Programs\Python\Python36-32\

ps > python --version
Python 3.6.5

PS > python
Python 3.6.5 (v3.6.5:f59c0932b4, Mar 28 2018, 16:07:46) [MSC v.1900 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> for item in sys.path:
...     print(item)
...

G:\Users\<username>\AppData\Local\Programs\Python\Python36-32\python36.zip
G:\Users\<username>\AppData\Local\Programs\Python\Python36-32\DLLs
G:\Users\<username>\AppData\Local\Programs\Python\Python36-32\lib
G:\Users\<username>\AppData\Local\Programs\Python\Python36-32
G:\Users\<username>\AppData\Local\Programs\Python\Python36-32\lib\site-packages
>>> exit()

```

##  2. pip installation

- pip�́Apython 3.4���C���X�g�[���ɓ�������Ă���B���A��L�ŁApath���ʂ��Ă���΁A�N���ł���B
- pip���A�o�[�W�����A�b�v����B (powershell�͊Ǘ��Ҍ����ŋN������) ``` pip install --upgrade pip```

- �ȉ��Apowershell�Ŋm�F�B

``` powershell
ps > pip install --upgrade pip
PS > ls G:\users\<username>\AppData\Local\Programs\Python\Python36-32\Scripts\

    Directory: G:\users\<username>\AppData\Local\Programs\Python\Python36-32\Scripts

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/28/2018   9:09 PM          89494 easy_install-3.6.exe
-a----        5/28/2018   9:09 PM          89494 easy_install.exe
-a----        5/28/2018   9:09 PM          89466 pip.exe
-a----        5/28/2018   9:09 PM          89466 pip3.6.exe
-a----        5/28/2018   9:09 PM          89466 pip3.exe

PS > pip --version
pip 10.0.1 from cusersusernameappdatalocalprogramspythonpython36-32libsite-packagespip (python 3.6)
```

##  3. virtualenv / virtualenvwrapper-win installation

- virtualenv  virtualenvwrapper-win ��install

``` powershell
ps > pip install virtualenv
ps > pip install virtualenvwrapper-win
```

- �ȉ��Apowershell�Ŋm�F�B

``` powershell
PS > virtualenv --version
16.0.0
PS > virtualenvwrapper
 virtualenvwrapper is a set of extensions to Ian Bicking's virtualenv
 tool.  The extensions include wrappers for creating and deleting
 virtual environments and otherwise managing your development workflow,
 making it easier to work on more than one project at a time without
 introducing conflicts in their dependencies.

 virtualenvwrapper-win is a port of Dough Hellman's virtualenvwrapper to Windows
 batch scripts.

 Commands available:

   add2virtualenv: add directory to the import path
   cdproject: change directory to the active project
   cdsitepackages: change to the site-packages directory
   cdvirtualenv: change to the $VIRTUAL_ENV directory
   lssitepackages: list contents of the site-packages directory
   lsvirtualenv: list virtualenvs
   mkproject: create a new project directory and its associated virtualenv
   mkvirtualenv: Create a new virtualenv in $WORKON_HOME
   rmvirtualenv: Remove a virtualenv
   setprojectdir: associate a project directory with a virtualenv
   toggleglobalsitepackages: turn access to global site-packages on/off
   virtualenvwrapper: show this help message
   whereis: return full path to executable on path.
   workon: list or change working virtualenvs

```

- check installed modules.

``` powershell
PS > ls G:\users\<username>\AppData\Local\Programs\Python\Python36-32\Scripts\

    Directory: G:\users\<username>\AppData\Local\Programs\Python\Python36-32\Scripts

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       11/18/2017   8:13 AM           1805 add2virtualenv.bat
-a----         8/4/2017   8:30 PM             83 cd-.bat
-a----        11/9/2017   5:59 AM            823 cdproject.bat
-a----         8/4/2017   8:30 PM            368 cdsitepackages.bat
-a----         8/4/2017   8:30 PM            350 cdvirtualenv.bat
-a----        5/28/2018   9:09 PM          89494 easy_install-3.6.exe
-a----        5/28/2018   9:09 PM          89494 easy_install.exe
-a----        11/9/2017   5:59 AM            495 folder_delete.bat
-a----         8/4/2017   8:30 PM            997 lssitepackages.bat
-a----         8/4/2017   8:30 PM            267 lsvirtualenv.bat
-a----        12/8/2017   4:24 AM           1601 mkproject.bat
-a----       11/18/2017   9:07 AM           9122 mkvirtualenv.bat
-a----        5/28/2018   9:31 PM          93060 pip.exe
-a----        5/28/2018   9:31 PM          93060 pip3.6.exe
-a----        5/28/2018   9:31 PM          93060 pip3.exe
-a----       11/18/2017   9:02 AM           1050 rmvirtualenv.bat
-a----       11/18/2017   8:40 AM           2248 setprojectdir.bat
-a----         8/4/2017   8:30 PM            422 toggleglobalsitepackages.bat
-a----        5/28/2018   9:36 PM          93057 virtualenv.exe
-a----        11/9/2017   6:03 AM           2321 virtualenvwrapper.bat
-a----        12/8/2017   4:23 AM           1608 vwenv.bat
-a----        11/9/2017   5:59 AM            557 whereis.bat
-a----       11/18/2017   8:55 AM           1495 workon.bat

```

##  4. �v���W�F�N�g�p��python���𐶐�

- python�ł́Apip�ŃC���X�g�[�������O���p�b�P�[�W�́Alibsite-packages�ɔz�u�����B���A�v���W�F�N�g���ƂɃC���X�g�[������p�b�P�[�W�����Ǘ�����ꍇ�Avirtualenv�𗘗p����B
- virtualenv�ɁAwrap���Ďg���₷�������̂��Avirtualenvwrapper-win�ƂȂ�B
- �ȉ��̊��ϐ���ݒ�B
-- WORKON_HOME  : python����z��
-- PROJECT_HOME : Project����z��

- �ȉ��Apowershell�Ŋm�F�B

``` powershell
PS G:\> dir Env: | out-string -stream | select-string "WORKON|PROJECT"

PROJECT_HOME                   G:\workplace\py
WORKON_HOME                    G:\env\py
```

- ����A�g�p����command�́A�ȉ��B�v���W�F�N�g���Ɓi��repository���Ɓj�Ɋ��𕪂��邱�Ƃɂ���B

|command |function|note|
|--------|--------|-----------|
|workon|���ꗗ�\��||
|workon <envname>|���̐؂�ւ�|���Ȃ����A���삵�Ȃ��I|
|mkproject <envname>|�v���W�F�N�g���̍쐬||
|rmvirtualenv <envname>|���̍폜||
|lssitepackages|ls �O���p�b�P�[�W||
|lsvirtualenv|ls ��||
|virtualenvwrapper|help||
|whereis <filename>|�t�@�C�����̂̕\��||


- workon envname�����삵�Ȃ��̂ŁAactivate�́A�ȉ��Ŏ��s�B

``` powershell
PS > cd $Env:WORKON_HOME
PS > G:\env\py .<envname>\Scripts\activate
(<envname>) PS > 
```

###  4.1 sample���𐶐�

- mkproject�ŁAproject�𐶐�����ƁAWORKON_HOME��PROJECT_HOME�Ɋ������������B

```
PS G:\env\py> mkproject pysample
Using base prefix 'g:\\users\\sakai\\appdata\\local\\programs\\python\\python36-32'
New python executable in G:\env\py\pysample\Scripts\python.exe
Installing setuptools, pip, wheel...done.

    "G:\workplace\py\pysample" is now the project directory for
    virtualenv "G:\env\py\pysample"

    "G:\workplace\py\pysample" added to
    G:\env\py\pysample\Lib\site-packages\virtualenv_path_extensions.pth

PS > cd $Env:WORKON_HOME
PS > ls

    Directory: G:\env\py

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/1/2018   6:20 AM                pysample


PS G:\env\py> .\pysample\Scripts\activate
(pysample) PS G:\env\py> cd $Env:PROJECT_HOME
(pysample) PS G:\workplace\py> ls

    Directory: G:\workplace\py

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/1/2018   6:20 AM                pysample

```

- �ȉ��Apython�Ŋm�F�B

```
(pysample) PS G:\workplace\py> python
Python 3.6.5 (v3.6.5:f59c0932b4, Mar 28 2018, 16:07:46) [MSC v.1900 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> for item in sys.path:
...     print(item)
...

G:\env\py\pysample\Scripts\python36.zip
G:\env\py\pysample\DLLs
G:\env\py\pysample\lib
G:\env\py\pysample\Scripts
g:\users\sakai\appdata\local\programs\python\python36-32\Lib
g:\users\sakai\appdata\local\programs\python\python36-32\DLLs
G:\env\py\pysample
G:\env\py\pysample\lib\site-packages
G:\workplace\py\pysample
>>> exit()

```

- �ȉ��Avirtualenvwrapper�ɂĊm�F�B

```
(pysample) PS G:\workplace\py> lssitepackages

dir /b "G:\env\py\pysample\Lib\site-packages"
==============================================================================
easy_install.py
pip
pip-10.0.1.dist-info
pkg_resources
setuptools
setuptools-39.2.0.dist-info
virtualenv_path_extensions.pth
wheel
wheel-0.31.1.dist-info
__pycache__

G:\env\py\pysample\Lib\site-packages\easy-install.pth
==============================================================================
The system cannot find the file specified.

G:\env\py\pysample\Lib\site-packages\virtualenv_path_extensions.pth
==============================================================================
G:\workplace\py\pysample

(pysample) PS G:\workplace\py> lsvirtualenv

dir /b /ad "G:\env\py"
==============================================================================
pysample

(pysample) PS G:\workplace\py> workon

Pass a name to activate one of the following virtualenvs:
==============================================================================
pysample

```

###  4.2 sample�����폜

- �ȉ��Avirtualenv���Adeactivate���A���폜�B
```
(pysample) PS G:\workplace\py> deactivate
PS G:\workplace\py> rmvirtualenv pysample

    Deleted G:\env\py\pysample

PS G:\workplace\py>
```
{code}

- �Ȃ��APROJECT_HOME����PROJECT�t�H���_�́A�K�X�A�폜����B


## �T�D�܂Ƃ�
- �ȏ�Apython���\�z�ŁAvituralenvwrapper�𗘗p���āA���z�����\�z���āA�폜����菇���L�q�����B

// --- end of markdown


