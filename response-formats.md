# Response-format

## Svar från routes

Från routes returneras JSON-objekt med fälten `content` och `meta` (HATEOAS)

```
{
	content: {
		id: P12332,
		firstName: “Test”,
		…
	},
 	meta: {
		self: “/contacts/P12332”
		leases: “/contacts/P12332/leases”
		pages: 1,
		pageSize: 1
	}
}
```

## Fel från routes

Vi fel i anrop till routes, används felstruktur från RFC 7807

```
{
	"type": "applicant-not-found",
	"title": "Applicant not found",
	"status": 404,
	"detail": "Applicant not found for this rental object",
	"instance": "/rental-objects/101-11341-14/applicants/P1234567"
}
```

## Svar från adapters till services
