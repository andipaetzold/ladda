# Configuration

There are a handful optional options to configure Ladda. In a minimal configuration you need to specify at least **api** on the entity and **operation** on the method.

## Entity Configuration

* **ttl**: How long to cache in seconds. Default is `300` seconds.

* **invalidatesOn**: `[Operation]` where `Operation := "CREATE" | "READ" | "UPDATE" | "DELETE" | "NO_OPERATION"`. Default is `["CREATE", "UPDATE", "DELETE"]`.

* **invalidates**: `[EntityName]` where EntityName is the key of your EntityConfig. By default an empty list `[]`.

* **viewOf**: `EntityName`. Only specify if this is a subset for another entity (all fields must exist in the other entity).

* **api** (required): An object of ApiFunctions, functions that communicate with an external service and return a Promise. The function name as key and function as value.

* **enableDeduplication**: `true | false` Enables [deduplication](/docs/advanced/Deduplication.md)
  of all "READ" operations for this entity. Defaults to true.

## Method Configuration

* **operation**: `"CREATE" | "READ" | "UPDATE" | "DELETE" | "NO_OPERATION"`. Default is `"NO_OPERATION"`.

* **invalidates**: `[ApiFunctionName]` where ApiFunctionName is a name of another function in the same api (see Entity Configuration - api). By default this is the empty list `[]`.

* **idFrom**: `"ENTITY" | "ARGS" | Function`. Where `"ARGS"` is a string telling Ladda to generate an id for you by serializing the ARGS the ApiFunction is called with. "ARGS" will also tell Ladda to treat the value as a BlobValue. Function is a function `(EntityValue -> ID)`. By default "ENTITY".

* **byId**: `true | false`. This is an optimization that tells Ladda that the first argument is an id. This allows Ladda to directly try to fetch the data from the cache, even if it was acquired by another call. This is useful if you previously called for example "getAllUsers" and now want to fetch one user directly from the cache. By default false.

* **byIds**: `true | false`. Another optimization which tells Ladda that
  the first argument is a list of ids. Ladda will try to make an optimal
call (if any), looking up items from the cache and only calling for
items that are not yet present. Defaults to false.

* **enableDeduplication**: `true | false` Enable [deduplication](/docs/advanced/Deduplication.md)
  a "READ" operation. Defaults to true.

## Ladda Configuration

* **idField**: Specify the default property that contains the ID. By default this is `"id"`.

* **enableDeduplication**: `true | false` Enable [deduplication](/docs/advanced/Deduplication.md)
  of "READ" operation for all entities. Defaults to true.
