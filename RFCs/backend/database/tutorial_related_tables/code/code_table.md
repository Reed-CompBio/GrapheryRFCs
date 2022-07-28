# `Code` Table

The `Code` table describes runnable code snippets.

## Mixins

* [`UUIDMixin`](/RFCs/backend/database/mixins.md#UUIDMixin)
* [`TimeDateMixin`](/RFCs/backend/database/mixins.md#TimeDateMixin)

## Fields

|       Field       |                             Type                             |                  Description                   |
| :---------------: | :----------------------------------------------------------: | :--------------------------------------------: |
|      `name`       |                      `models.TextField`                      | The human readable name for this code snippet  |
|      `code`       |                      `models.TextField`                      |                The code snippet                |
| `tutorial_anchor` | [`OTO(TutorialAnchor)`](/RFCs/backend/database/tutorial_related_tables/tutorial/tutorial_anchor_table.md) | The tutorial associated with this code snippet |

## Code Snippet Guidelines

This describes behaviors of code acceptable by 3.0 API. For 2.0 API, please consult the older document.

After the 3.0 API, the graph and network library `networkx` are injected automatically as `nx` and `networkx`, and users can use it directly, so there is no need to import additional graph or library. With that said, following header should be appended to every code, in which `graph` variable is stated in the environment, and the upcoming code should only use `graph` to refer to the tutorial graph. This is because users can apply the tutorial algorithms by coping the whole tutorial code and replacing `graph` with any other `networkx` graph, without changing anything else.

**UPDATE**: The following header and tail will not be added but rather written manually. 

```python
# Python Version: <the python version of the executor>
# Executor Version: <the version of the executor>
from __future__ import annotations 

import networkx as nx 
graph: nx.Graph
# graph is injected automatically and refers to the tutorial graph
```

Due to the structural change of the executor, the "main" entrance must be stated in the end for a code to be executed. For example: 

```python
if __name__ == '__main__':
  # do something here 
  pass
```

The header should not appear in the database, but rather added during the runtime request. That is, suppose the algorithm looks like the following

```python
def main():
  	# an algorithm for looping through all the code
		for node in graph.nodes:
    		print(node)
```

The code displayed in the frontend should be

```python
# Python Version: <the python version of the executor>
# Executor Version: <the version of the executor>
from __future__ import annotations 

import networkx as nx 
graph: nx.Graph
# graph is injected automatically and refers to the tutorial graph

def main():
  	# an algorithm for looping through all the code
		for node in graph.nodes:
    		print(node)

if __name__ == '__main__':
  	# do something here 
  	main()
```

All the code will be lint with [`black`](https://github.com/psf/black) in the backend before being stored into the database.

