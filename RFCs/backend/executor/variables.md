# Variables

## Environment Variables

The executor uses a bunch of environment variables to determine the content it serves. Every environment variable is listed below and when used in shell environment, each should be prefixed with  `GE_`  which is short for graphery executor. For example, if the server port is to be set ot `23032`, `export GE_SERVER_PORT=23032` can be used.

|     Variable     | Default Value |                         Description                          |
| :--------------: | :------------: | :----------------------------------------------------------: |
|   `SERVER_URL`   |  `127.0.0.1`   |         The URL used to access the executor server.          |
|   `SERVER_PORT`   |     `7590`     |         The port used to access the executor server.         |
| `ALLOW_OTHER_ORIGIN` | `True` | If other origins are allowed other than `ACCEPTED_ORIGINS` |
| `ACCEPTED_ORIGINS` |     `['127.0.0.1']`     |      The allowed origins that can access the executor server.      |
| `LOGGER` | `shell_info_logger` | Info level logs are displayed on shell by default. |
| `EXEC_TIME_OUT`  |      `5`       | The time, in seconds, during which the executor is allowed to run. |
| `EXEC_MEM_OUT` | `100` | The size, in Mb, which the program can occupy. |
|      `IS_LOCAL`      |     `False`     |    Indicator of whether the script is running locally. If this is turned on, the server ignores every security check.    |
| `RAND_SEED` | `0` | The default random seed used in simulation. `None` or integers can be used. |
| `FLOAT_PRECISION` | `4` | The number of float precision. Integers can be used. |

|          Variable           | Default Value |                   Description                    |
| :-------------------------: | :-----------: | :----------------------------------------------: |
|  `REQUEST_DATA_CODE_NAME`   |    `code`     |  The name of code field in the request object.   |
|  `REQUEST_DATA_GRAPH_NAME`  |    `graph`    |  The name of graph field in the request object.  |
| `REQUEST_DATA_VERSION_NAME` |   `version`   | The name of version field in the request object. |
| `REQUEST_DATA_OPTIONS_NAME` |   `options`   | The name of options field in the request object. |

## Docker Environment Variables

|          Variable          |  Default Value   |                         Description                          |
| :------------------------: | :--------------: | :----------------------------------------------------------: |
|  `GE_DOCKER_RESTART_COND`  | `unless-stopped` | Indicate which stop policy the docker should implement. [REF](https://docs.docker.com/compose/compose-file/compose-file-v3/#restart_policy) |
| `GE_DOCKER_RESTART_WINDOW` |       `10`       | The unit is `s`econd. The time docker should wait before deciding if the restart has succeeded or not. [REF](https://docs.docker.com/compose/compose-file/compose-file-v3/#restart_policy) |
|    `GE_DOCKER_MEM_OUT`     |       `32`       | The unit is `M`egibyte. The maximum amount of memory docker image can take. Exceeding the limit will issue system kill. |
|    `GE_DOCKER_CPU_OUT`     |      `0.10`      | The unit is `%`. The percentage of CPU the container can use. |

## Custom Variables

Custom variables are variables referenced within executor and are not intended to be modified.

|         Variable          |        Value        |                         Description                          |
| :-----------------------: | :-----------------: | :----------------------------------------------------------: |
|        `PROG_NAME`        | `graphery_executor` | The program name used by pip executable and internal server. |
|     `SERVER_VERSION`      |       `3.0.0`       | The version of this server. The first digit of the server version matches the version of the result JSON API version. |
|  `IDENTIFIER_SEPARATOR`   |     `"\u200b@"`     |          The identifier separator used by recorder.          |
|  `GRAPH_INJECTION_NAME`   |       `graph`       | The name the tutorial graph take when injected into the execution environment. |
| `NX_GRAPH_INJECTION_NAME` |      `g_graph`      | The name the tutorial graph take when injected into the `networkx` module. |

## Error Code

The exit code return by executor when running locally.

|      Variable       | Value |                         Description                          |
| :-----------------: | :---: | :----------------------------------------------------------: |
|  `CTRL_ERROR_CODE`  |  `3`  | Some error happened within controller and should be reported to maintainers. |
|  `INIT_ERROR_CODE`  |  `5`  | Some error happened within the controller  `init` process. This is mostly caused by erroneous input. |
|  `PREP_ERROR_CODE`  |  `7`  | Some error happened within the controller `prep` process. They are mostly issues from controller. |
|  `POST_ERROR_CODE`  | `11`  | Some error happened within the controller `post` process. They are also mostly issues from controller. |
| `RUNNER_ERROR_CODE` | `13`  | Some error happened during running user code. This is caused by user-provided script. |
| `CPU_OUT_EXIT_CODE` | `17`  |            This indicates the CPU time runs out.             |
| `MEM_OUT_EXIT_CODE` | `19`  |       This indicates the allocated Memory is consumed.       |

## Shell Args

|          Variable          |  Value   |                         Description                          |
| :------------------------: | :------: | :----------------------------------------------------------: |
| `SHELL_PARSER_GROUP_NAME`  | `WHERE`  | The `Namespace` attribute name of the executor mode, the value should be either value below. |
| `SHELL_SERVER_PARSER_NAME` | `server` | A possible value of `WHERE`, indicating the running mode is server mode. |
| `SHELL_LOCAL_PARSER_NAME`  | `local`  | A possible value of  `WHERE`, indicating the running mode is local mode. |
