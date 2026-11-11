---
type: regex
target: last_message
pattern: 'sketchmonkey(?:\.|_{1,2}|\s)neuraldeepnet|sketchmonkeyneuraldeepnet|/cdn/sketchmonkey-neuraldeepnet|adaptive\.ai/sketchmonkey/|/cdn/(?!sketchmonkey/)[^/\s)]+/'
match: not_contains
---
