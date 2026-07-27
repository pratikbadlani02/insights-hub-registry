# Business Rules

> Project: spring-petclinic1
> Type: rest-api
> Skill: spring-analysis
> Analyzed: 2026-06-28T00:00:00Z

---

## Entity Lifecycle

```
NEW (id == null) --[owners.save]--> PERSISTED (id assigned)
PERSISTED --[edit + save]--> PERSISTED (updated)
```

New-vs-existing is determined by `BaseEntity#isNew()` (id null) — `model/BaseEntity.java:47`.

## Rule Sets

**Rule Set 1: Owner**
- `firstName`, `lastName`, `address`, `city` required; not blank (`owner/Owner.java`, `model/Person.java`).
- `telephone` must match `\d{10}` (`owner/Owner.java`).
- Edit rejects when form `ownerId` ≠ URL `ownerId` (`OwnerController#processUpdateOwnerForm:149`).
- `id`/`*.id` fields disallowed from binding (`OwnerController#setAllowedFields:60`).

**Rule Set 2: Pet** (`owner/PetValidator.java`, `PetController.java`)
- Name required; type required only when pet is new; birth date required.
- Birth date may not be in the future (`PetController:115`).
- Duplicate pet name per owner rejected (`PetController:110`, `:143`).

**Rule Set 3: Visit** (`owner/VisitController.java`)
- `description` not blank (`owner/Visit.java:42`).
- Visit date must be after today (`VisitController:100`); default is tomorrow (`Visit:48`).

**Rule Set 4: Vet listing**
- Paginated 5 per page; full list cacheable as `vets` (`VetController:62`, `VetRepository:46`).

## Search Rules

- `/owners` last-name search uses `findByLastNameStartingWith`; empty = broadest; 1 result redirects to detail; 0 rejects with `notFound` (`OwnerController:94`).

## Feature Toggles

N/A — no feature-flag system (e.g. LaunchDarkly) present in source.
