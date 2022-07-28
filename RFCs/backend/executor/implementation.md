# Implementation

## `executor`

`executor` is the name of the module executing user-provided scripts on a particular networkx graph. It has two modes: `local` and `server`. To use the executor, the module should be installed by pip and `graphery_executor` executable will be available for execution. `graphery_executor -h` can be used to check the supported options and `graphery_executor -V` can be used to check the installed version.

The `local` mode uses `stdin` as the input source. The supported API is listed in [`./local/API.md`](./local/API.md). When executed successfully, a formatted json will be printed to `stdout`, and error messages and stacktrace if otherwise.

The `server` opens up a WSGI server on specified `host` and `port`, which are defaulted to `127.0.0.1` and `7590` respectively. The server accepts `POST` method when queries are posted to `/run` slug and `GET` method when `/env` is the target. When posting to `/run`, it should follow the local API, i.e. [`./local/API.md`](./local/API.md). When a message is received, the server creates a subprocess, hands the message to a `local` `executor`, wraps the `stdout` from `local` `executor`, and send back a response. The response is always `200 OK` except when the server goes wrong and `500 Internal Server Error` will be returned.

## `Controller`

A `Controller` is used in `local` `executor` and handles all the execution management. The `Controller` class takes in three 4 components: `runner`, `context_layers`, `default_settings`, `options`. The
controller is intended to execute the provided `runner` procedure within the context layers. The controller works in the
following way.

1. Instantiated by provided `runner`, `context_layers`,  `default_settings`,  `options`, and any keyword arguments. The
   controller then extracts required information from settings, options, and keyword arguments. Context layers are also
   initialized during this process.
2. After instantiation, the controller needs to go through `init` process to be usable. The process can be realized
   through `init` or `__call__` provided to controllers. The `init` process collects sets up the environment in which
   the `runner` with be performed, most notably the `user_global` which serves as the global environment for `runner`.
   If an error is raised during the `init` process, the `INIT_ERROR_CODE` will be used when program exits.
3. Then `main` procedure from the controller should be called. Once `main` is called, controller will go into `prep`
   process that prepares the variables, modules, and security procedures for `runner` and call `runner` if everything is
   good to go. `runner` is called by using `exec` with custom globals and locals made during `init` process and `prep`
   process. Any error happened in `prep` process will trigger `PREP_ERROR_CODE` and errors during running `runner` will
   trigger `RUNNER_ERROR_CODE`. If the `runner` successfully completes, the controller will go into `post` process so
   that it can clean up aftermath and remove security procedure.
4. `main` will return whatever is returned by `runner` if it completes successfully. Otherwise, `ErrorResult` is
   returned.

Some context layers are provided by default.

* `_RandomContext`  sets the random seed to a fix value and release it after exiting.
* `_FDRedirectLayer`  redirects `stdout` and `stderr` to some streams or file descriptors during executing `runner` and
  release them after exiting.
* `_ModuleRestrict`  restricts what modules can be imported in the `runner`.
* `_ResourceRestrict` restricts how much time and memory the runner can consume.

A list of options can be used in controller is provided below:

|    Name     |         Default Value         |                                                                                                                         Description                                                                                                                          |
|:-----------:|:-----------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|  `logger`   |    `LOGGER` from settings     |                                                                           Logger instance that will be in controller. When this is not set, the `LOGGER` in settings will be used.                                                                           |
| `custom_ns` |             `{}`              | Custom namespace that will be used in runner environment. The type should be a `Mapping`. For example, suppose the custom namespace is defined as `custom_ns = {'special': 'some_text'}`. Then, the runner code can reference `special` without defining it. |
|  `stdout`   |         `StringIO()`          |                                                                                     It's used to specified where the stdout will be captured during executing `runner`.                                                                                      |
|  `stderr`   |         `StringIO()`          |                                                                                                            Similar to `stdout`, but for `stderr`.                                                                                                            |
| `formatter` | `ControllerResultFormatter()` |                                                                            A formatter specifying how the controller result will be modified. There is no other options for now.                                                                             |

## `GraphController`

`GraphController` is a subclass of `Controller`. The `runner` baked into the class and should not be provided by caller.
But it takes in two additional keyword only arguments: `code` and `graph_data`. The `GraphController` behaves the same
as a `Controller` except a few more steps in `init` process: it also builds a networkx  `graph` from `graph_data`, sets
up a `Recorder` and then make a copy of `tracer`; it then injects `networkx`,  `graph`, and `tracer` to
the `user_globals` so that they can be referenced during the execution of  `code`.

## `ContextLayer`

The context layer behaves like a standard helper from `contextlib` and is intended to be used along `with` clause or in
controllers' `prep` process or `post` process. It implements `__enter__` and `__exit__` procedures and have
explicit `enter` and `exit` procedures available. A context layer takes a controller instance as initialization
argument.

## `DefaultVars` (Settings)

The `DefaultVars` is used to store option variables and to read and sets values from environment variables if there is
any. All variables are listed in the first second of [`variables.md`](./variables.md). The `DefaultVars` and it's
instance support `__getitem__` procedure. When a setting name is provided, the corresponding value will be returned
by `[]` operation. It's cumbersome to write `setting[setting.IS_LOCAL]` so a getter is added, and it's possible to
achieve the same thing by using `setting.v.IS_LOCAL`. In `DefaultVars`, `read_from_env` is provided to read value from
shell environment variables.
