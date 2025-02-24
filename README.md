# pyxorfilter

[![Build Status](https://travis-ci.org/glitzflitz/pyxorfilter.svg?branch=master)](https://travis-ci.org/glitzflitz/pyxorfilter)

Python bindings for [C](https://github.com/FastFilter/xor_singleheader) implementation of [Xor Filters: Faster and Smaller Than Bloom and Cuckoo Filters](https://arxiv.org/abs/1912.08258)
## Installation
### From Source
```
git clone --recurse-submodules https://github.com/GreyDireWolf/pyxorfilter
cd pyxorfilter
python setup.py build_ext
python setup.py install
```
## Usage
```py
>>> from pyxorfilter import Xor8, Xor16
>>> filter = Xor8(5)	#or Xor16(size)
>>> #Supports unicode strings and heterogeneous types
>>> test_str = ["あ","अ", 51, 0.0, 12.3]
>>> filter.populate(test_str)
True
>>> filter.contains("अ")
True
>>> filter[51]  #You can use __getitem__ instead of contains
True
>>> filter["か"]
False
>>> filter.contains(150)
False
>>> filter.size_in_bytes()
60
```
## Caveats
### Accuracy
For more accuracy(less false positives) use larger but more accurate Xor16.
### Overflow
Both Xor8 and Xor16 take uint8_t and uint_16t respectively. Make sure that the input is unsigned.

### TODO

- [x] Add unit tests
- [ ] Add CI support for distributing pyxorfilter with PyPI.

## Links
* [C Implementation](https://github.com/FastFilter/xor_singleheader)
* [Go Implementation](https://github.com/FastFilter/xorfilter)
* [Erlang bindings](https://github.com/mpope9/exor_filter)
* Rust Implementation: [1](https://github.com/bnclabs/xorfilter) and [2](https://github.com/codri/xorfilter-rs)
* [C++ Implementation](https://github.com/FastFilter/fastfilter_cpp)
* [Java Implementation](https://github.com/FastFilter/fastfilter_java)
