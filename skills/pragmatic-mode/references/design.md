# Design

## Extend before adding

- Make the minimal, surgical change. Extend or refactor current systems rather
  than adding new ones.
- Extend an existing resource rather than adding operation-specific entry
  points. Extend the CRUD of the REST resource `/machine` instead of creating
  `/machine/cooling` or `/machine/display`.

## Deep modules

Keep each module's external API minimal and stable, with a small surface.
Handle complexity inside the internal services, and keep those services KISS,
DRY, and SOLID.

## Data

- Avoid database changes. When the information can be read from existing data,
  or generated or inferred at runtime, do that instead.
- Extend existing models before creating new ones.
- Keep the data normalized up to third normal form.

## No backward compatibility

When you change or replace a path, move every live caller to the new
implementation and remove the obsolete path in the same change. Do not add
compatibility layers, fallbacks, or mitigations. Untouched legacy code may stay
until work brings it into scope.
