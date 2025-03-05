# Routes - namngivning och principer

Som grundprincip utgår vi från DIGGs REST API-profil: https://www.dataportal.se/rest-api-profil

## Namngivning av routes

https://www.dataportal.se/rest-api-profil/url-format-och-namngivning

- En resurs (första delen av sökvägen, grundsökväg eller endpointprefix), t.ex. /contacts, hanteras i
  källkoden av en service. Varje grundsökväg ska ha en egen service, som namnges på ett sätt som gör det lätt
  att förstå vilken grundsökväg som hanteras - t.ex. resursen **/contacts hanteras av
  services/contact-service**
- Resursen är alltid ett substantiv i pluralform - **/contacts**, inte /contact eller /get-contact
- `GET /resurs` ger lista av alla sådana resurser, t.ex. `GET /contacts`.
- `POST /resurs` skapar en sådan resurs, t.ex. `POST /contacts`.
- Filter skickas som query-parametrar: ?fields, ?filter, ?sort, ?page
- Alla routes ska använda gemener, och ord separeras med bindestreck, t.ex. `/work-orders, inte /workOrders`
- Varje resurs har en kanonisk identifierare. `GET /resurs/identifierare` returnerar den resursen, t.ex.
  `GET /contacts/P1234567`.
- Om en endpoint hämtar en resurs via icke-kanonisk identifierare används ett förklarande url-segment, t.ex.
  `GET /contacts/by-phone-number/070123456`
- Om relaterade resurser hämtas läggs url-segment till efter kanoniska url:en `GET /contacts/P1234567/leases`

## Versionshantering

- Vi försöker lösa breaking changes med versionshantering för att
- Vi versionerar varje route för sig. `GET /v2/contacts/P1234567` kan samexistera med `GET /v3/leases` och
  `GET /contacts/P1234567/leases`.
- När en ny version av en route skapas, markeras den tidigare versionen i källkoden som obsolete.

### Hypermedialänkar (HATEOAS)

https://www.dataportal.se/rest-api-profil/hypermedia

I onecore-utilites finns hjälpfunktioner för att automatiskt skapa HATEOAS-länkar i route-svar
(generateMetaData)
