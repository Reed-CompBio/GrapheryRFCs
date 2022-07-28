# Result JSON Meta API

## API Versions

* [3.0](#3-0)

## 3.0 API {#3-0}

```typescript
interface breakpoints_type {
    [key: number]: string;
    // the key is the line number 
    // the value is the corresponding tag
}

interface result_json_meta_type {
    version: string;
    breakpoints: breakpoints_type;
}
```
