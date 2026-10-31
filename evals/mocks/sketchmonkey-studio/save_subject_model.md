---
expect:
  name: string
  kind: [object, car, space, character, creature]
  identityLock: string
---

{"id":"sm_mock_001","name":"{{input.name}}","kind":"{{input.kind}}","saved":true,"note":"Saved reference data; this does not train a model or guarantee identical results."}
