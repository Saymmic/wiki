
### [Alex Orlov Cython as a Game Changer for Efficiency PyCon 2017](https://www.youtube.com/watch?v=_1MSX7V28Po)

For simple solutions with small number of machines is no need for optimization you just add additional boxes. Readability and simplicity first.
If you have big enough infrastructure then think about optimization

1. Check algorithm first and check all options for pure python solutions
2. Extract piece of functionality and rewrite it as a microservice in faster language
3. Create lib in c++ rewrite some functionality and plug it to your python code
4. Use some alternative interpreter eg. pypy GrumPy ... ( probably need some migrations)
5. Sometimes updating CPython is the case
6. Adjust your code to Cython

### [Greg Price - Clearer Code at Scale: Static Types at Zulip and Dropbox - PyCon 2018](https://www.youtube.com/watch?v=0c46YHS3RY8)

Dropbox (2MLOC +) and Zulip and also instagram are using type annotations.

1. **mypy** for type annotation checking -> use it with your hooks with script (see Zulip script for mypy)

**Tools**
  * **MonkeyType** (facebook/instagram) - Tries to annotate functions automaticly in runtime (instagram using it in production)
  * **PyAnnotate** (dropbox) - same as above
  * **pytype** (google) - Statically check and infer types for unannotated Python code. (This is not an official Google product.)
