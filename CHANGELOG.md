# Change Log
All notable changes to this project will be documented in this file.

## Pointer fields

Pointer fields are no longer assigned to by default.

For example, previously an empty value (`[]string{""}`) for a `*int` would result in that field being set to `*0`

Now pointer fields will remain `nil` for empty values, e.g.

```go
type Form struct {
    Field *int
}

var form Form

err = schema.NewDecoder().Decode(&form, url.Values{})

if err != nil {
    // Handle error
}

// Here form.Field == nil, not *0
```