[![tests](https://github.com/mjx-project/mjx-convert/actions/workflows/tests.yml/badge.svg)](https://github.com/mjx-project/mjx-convert/actions/workflows/tests.yml)

# mjx-convert

Convert Mahjong log into another format.

ref:
https://note.com/oshizo/n/n61441adc340c

## prerequisite

for macOS

```sh
$ brew install ninja
```

ninja と cmake 入れても動かない。。。(make install)

```
❯ make install
python3 setup.py install
running install
/Users/oonuma/.anyenv/envs/pyenv/versions/3.11.3/lib/python3.11/site-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
/Users/oonuma/.anyenv/envs/pyenv/versions/3.11.3/lib/python3.11/site-packages/setuptools/command/easy_install.py:144: EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
running bdist_egg

略

  warnings.warn(
CMake Warning:
  Ignoring extra path from command line:

   "/private/var/folders/2q/m7cxsq7n0rn3v9nm_31kjhtr0000gn/T/easy_install-h1md9fkb/tenhou_wall_reproducer-1.2.0"


CMake Error: The source directory "/private/var/folders/2q/m7cxsq7n0rn3v9nm_31kjhtr0000gn/T/easy_install-h1md9fkb/tenhou_wall_reproducer-1.2.0" does not appear to contain CMakeLists.txt.
Specify --help for usage, or press the help button on the CMake GUI.
Traceback (most recent call last):
  File "/Users/oonuma/.anyenv/envs/pyenv/versions/3.11.3/lib/python3.11/site-packages/setuptools/sandbox.py", line 156, in save_modules
    yield saved
    〜〜略〜〜
    self.build_extension(ext)
  File "/var/folders/2q/m7cxsq7n0rn3v9nm_31kjhtr0000gn/T/easy_install-h1md9fkb/tenhou_wall_reproducer-1.2.0/setup.py", line 103, in build_extension
  File "/Users/oonuma/.anyenv/envs/pyenv/versions/3.11.3/lib/python3.11/subprocess.py", line 413, in check_call
    raise CalledProcessError(retcode, cmd)
subprocess.CalledProcessError: Command '['cmake', '/private/var/folders/2q/m7cxsq7n0rn3v9nm_31kjhtr0000gn/T/easy_install-h1md9fkb/tenhou_wall_reproducer-1.2.0', '-DCMAKE_LIBRARY_OUTPUT_DIRECTORY=/private/var/folders/2q/m7cxsq7n0rn3v9nm_31kjhtr0000gn/T/easy_install-h1md9fkb/tenhou_wall_reproducer-1.2.0/build/lib.macosx-13.4-arm64-cpython-311/', '-DPYTHON_EXECUTABLE=/Users/oonuma/.anyenv/envs/pyenv/versions/3.11.3/bin/python3', '-DEXAMPLE_VERSION_INFO=1.2.0', '-DCMAKE_BUILD_TYPE=Release', '-GNinja']' returned non-zero exit status 1.
make: *** [install] Error 1

```

## Install

```sh
$ make install
```

## Example

### Using stdin

```sh
$ cat test.mjlog | mjxc convert --to-mjxproto
$ cat test.mjlog | mjxc convert --to-mjxproto-raw
$ cat test.json  | mjxc convert --to-mjlog
```

### Using file inputs

```sh
$ mjxc convert ./mjlog_dir ./mjxproto_dir --to-mjxproto
$ mjxc convert ./mjlog_dir ./mjxproto_dir --to-mjxproto-raw
$ mjxc convert ./mjxproto_dir ./mjlog_dir --to-mjlog
```

## Note

- File inputs assume that each file corresponds to each game in any format.
- Difference between mjxproto and mjxproto-raw:
  1. Yaku is sorted in yaku number
  2. Yakuman's fu is set to 0
