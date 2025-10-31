# UFAClient: list_files_in_dir

```python
from ufa.client import UFAClient

client = UFAClient(
    base_url="https://api.edge.deeporigin.io/files/",
    token="...",
    org_key="deeporigin",
)

listing = await client.list_files_in_dir(directory_path="tests/ufa")
print(listing.get("continuationToken", ""))
for entry in listing.get("data", []):
    print(entry["Key"], entry["Size"])  # example fields
```

This maps to the HTTP GET endpoint:

```
GET https://api.edge.deeporigin.io/files/{org_key}/directory/{percent_encoded_prefix}
```

Where the `directory_path` is percent-encoded as a single path segment (slashes are encoded).

Optional parameters:

- `continuation_token`: Pass to continue a previous listing
- `max_keys`: Limit the number of items returned (if supported)

The returned JSON has fields similar to:

```json
{
  "data": [
    {"Key": "tests/ufa/ligand.sdf", "Size": 123, "LastModified": "..."}
  ],
  "continuationToken": ""
}
```


