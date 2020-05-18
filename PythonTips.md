# Python Tips

## Cython

[Cython](https://cython.org/)
[Cython Documentation](https://cython.readthedocs.io/en/latest/index.html)

### Install cython

```sh
$ conda install cython
```

or

```sh
$ pip install Cython
```

Note the difference of `cython` and `Cython`

### Install Visual C++

[Visual Studio 2019 Community](https://visualstudio.microsoft.com/downloads/)
or
[Microsoft C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

At minimal, you need (you can choose the latest version number):
- MSVC v142 – VS 2019 C++ x64/x86 build tools (v14.25)
    this will provide `vcvarsall.bat` in `c:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build`
- Windows 10 SDK (10.0.19041.0)
    this will provide `basetsd.h` in `c:\Program Files (x86)\Windows Kits\10\Include\10.0.19041.0\shared`

### Try it

#### Using setup

Write a simple python code with .pyx extension, like below `hellocython.pyx`
```py
print('Hello Cython!')
```

Write a setup file like below `setup.py`
```py
from setuptools import setup
from Cython.Build import cythonize

setup(
    ext_modules = cythonize("hellocython.pyx")
)
```

run command
```sh
$ python setup.py build_ext --inplace
```

it will generate a `.pyd` file like `hellocython.cp37-win_amd64.pyd`, so you can import it as normal python package

```py
>>> import hellocython
Hello Cython!
```

#### Simply using cythonize

Write `fib.pyx`

```pyx
def fib(n):
    a, b = 0, 1
    while b < n:
        print(b, end=' ')
        a, b = b, a + b
    print()
```

run command

```sh
$ cythonize fib.pyx -3 -i -a
```

run python to import `fib.cp37-win_amd64.pyd`

```py
>>> from fib import fib
>>> fib(1000)
1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
```