---
created: 2022-07-11T22:57:00+08:00
modified: 2022-07-11T23:06:39+08:00
---

# Python ignore all exceptions and continue execute next line in given section of code

python grammar sugar: brackets
https://pypi.org/project/brackets/
does that work in eval()?

use contextlib.suppress to replace try...except: pass
might investigate source code of the suppress object.

https://opensource.com/article/18/5/how-retrieve-source-code-python-functions

to execute code grouped by lowest level of indentation, we can def those lines of code and pass the code by dill.source.getsource(functionName) and eval within given global/local variables.
