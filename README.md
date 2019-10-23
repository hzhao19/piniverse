# Piniverse

Piniverse is a simple library to programmatically orchestrate function calls for Python. 

<br>
  <p align="center">
    <img src="docs/static/pin.png" height="350" width="600" align="center">
  </p>
<br>

Table of contents
---------------

- [Features Support](#features-support)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Limitations](#limitations)
- [Contributions](#contributions)

Features Support 
---------------

* Execution of pinned functions inside a python package in topological ordering
* Visualization of the directed acyclic graph

Prerequisites 
---------------

* Python 3.7

Getting Started
---------------

### Installation

```
$ pip install piniverse
```

### Basic Usage

Piniverse inspects pinned functions inside a package

```
.
├── workspace/    <-- workspace directory
├── script.py     <-- script file

```

To orchestrate your desired functions, pin them! Every pinned function has a task identifier, and if applicable, a succeeding toward identifier.

```
# workspace/

from piniverse import Pinned


@Pinned(
  task='1',
  toward='2', 
  arguments={
    args: ['Hello World']
    kwargs: {'content': 'Programming exercise...'}
  }
)
def simple_print(title: str, content: str = '') -> None:
  message = """
    Title: {}
    Content: 
      {}
  """.format(title, content)
  
  print(message)


@Pinned(
  task='2',
  arguments={
    args: ['A pretty Hello World']
    kwargs: {'content': 'A pretty programming exercise!'
  }
)
def pretty_print(title: str, content: str = '') -> None:
  message = """
    Pretty Title: {}
    Pretty Content: 
      {}
  """.format(title, content)

  print(message)

```

To execute your pinned functions, plan and apply!

```
# script.py

import piniverse
import workspace


piniverse.plan(workspace)
piniverse.apply()

// Title: Hello World
// Content: 
//   Programming exercise...
// Title: A pretty Hello World
// Content:
//   A pretty programming exercise
```

### User Interface

Piniverse also provides a straightforward visualization of your task definitions. 

```
# script.py

pinverse.plan(workspace, plan_view=True)
```

<br>
  <p align="center">
    <img src="docs/static/visual.png" height="550" width="750" align="center">
  </p>
<br>

Limitations 
---------------

Presently, Piniverse solely supports standalone functions.

Contributions 
---------------

Contributions are more than welcome! Check out the [contribution documentation](https://github.com/hzhao19/piniverse/blob/master/CONTRIBUTIONS.rst).
