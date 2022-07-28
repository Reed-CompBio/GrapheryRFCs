# API

## Introduction

There are two sets of API, one for server mode and one for local mode. This API is for server mode. For local mode,
please check out [here](../local/API.md).

## 3.0 API

### Request

The request object looks like the following.

```typescript
interface request_object {
    code: string;
    graph: string | object;
    version: string;
    options?: request_options;
}

interface request_options {
    rand_seed?: int;
    float_precision?: int;
    input_list?: string[];
}

```

If any of the request options is undefined, we use the default options to make sure it doesn't have undefined fields.

```typescript
let default_request_options: request_options = {
    rand_seed: 0,
    float_precision: 4,
    input_list: []
}
```

### Response

where the `record_array_type` is defined in
the [`result JSON API`](/RFCs/backend/database/tutorial_related_tables/execution_result/result_json_api.md).

```typescript
type err_msg_type = {
    message: string;
    traceback: string;
};

type response_info_type = {
    result: record_array_type,
    [key: string]: any
}

interface response_object_type {
    info: response_info_type | null;
    errors: err_msg_type[] | null;
}

interface successful_response_object_type extends response_object_type {
    info: response_info_type
    errors: null;
}

interface error_response_object_type extends response_object_type {
    info: null;
    errors: err_msg_type[];
}
```
