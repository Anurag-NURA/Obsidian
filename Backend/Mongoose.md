### Nested Array field

Sometimes you may have field like these: 

```JSON
_id: ObjectId("4242424bsdfg323"),
name: "Anurag",
experience: [
	{ company: "Spotify", duration: 1 },
	{ company: "Google", duration: 3.4 }
]
```

These  are called  __Nested field__ (array of object in this case) and need more then just a simple query for updating records in this field.

__Updating Nested Array Field__

`db.users.find({ experience: {$elemMatch`
