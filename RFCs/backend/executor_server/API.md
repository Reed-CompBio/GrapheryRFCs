# API

## Introduction

There are two sets of API, one for incoming requests and one for responses.

## 3.0 API

### Request

The request object looks like the following.

```typescript
interface request_object {
    code: string;
    graph: string | object;
    options?: request_options;
}

interface request_options {
    version?: '3' | '2';
    rand_seed?: int;
    float_precision?: int;
    input_list?: string;
}

```

If any of the request options is undefined, we use the default options to make sure it doesn't have undefined fields.

```typescript
let default_request_options: request_options = {
    version: '3',
    rand_seed: 0,
    float_precision: 4,
    input_list: '',  // not decided yet 
}
```

### Response

where the `record_array_type` is defined in
the [`result JSON API `](/RFCs/backend/database/tutorial_related_tables/execution_result/result_json_api.md).

```typescript
type response_code_type = 'succ' | 'error';

type err_msg_type = string[];

interface response_object_type {
    code: response_code_type;
    exec_result: record_array_type | null;
    err_msg: err_msg_type | null;
}

interface successful_response_object_type extends response_object_type {
    code: 'succ';
    exec_result: record_array_type;
    err_msg: null;
}

interface error_response_object_type extends response_object_type {
    code: 'error';
    exec_result: null;
    err_msg: err_msg_type;
}
```
