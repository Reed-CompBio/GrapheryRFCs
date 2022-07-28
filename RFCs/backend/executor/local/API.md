# API

## Introduction

This API is for the local mode.

## 3.0

The local mode is started by shell. The usage is listed below.

```shell
usage: graphery_executor [-h] [-V] [-t EXEC_TIME_OUT] [-m EXEC_MEM_OUT] [-i] [-r RAND_SEED] [-f FLOAT_PRECISION]
                         [-l {void, shell_debug, shell_info}]
                         {server,local} ...

Graphery Executor Server

positional arguments:
  {server,local}

options:
  -h, --help            show this help message and exit
  -V, --version         show program's version number and exit
  -t EXEC_TIME_OUT, --time-out EXEC_TIME_OUT
  -m EXEC_MEM_OUT, --mem-out EXEC_MEM_OUT
  -i, --is-local
  -r RAND_SEED, --rand-seed RAND_SEED
  -f FLOAT_PRECISION, --float-precision FLOAT_PRECISION
  -l {void, shell_debug, shell_info}, --logger {void, shell_debug, shell_info}

```

The minimal command is `graphery_executor local`, and a piece of request data must be fed through stdin as input. For the format of request data, please check out [server API](../server/API.md), and the response is formatted as `record_array_type` which is detailed [here](/RFCs/backend/database/tutorial_related_tables/execution_result/result_json_api.md).
