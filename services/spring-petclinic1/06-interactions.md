# Interactions

> Project: spring-petclinic1
> Type: rest-api
> Skill: spring-analysis
> Analyzed: 2026-06-28T00:00:00Z

---

## Owner Search (happy path)

```mermaid
sequenceDiagram
  participant U as Browser
  participant OC as OwnerController
  participant OR as OwnerRepository
  participant DB as Database
  U->>OC: GET /owners?lastName=Smith&page=1
  OC->>OR: findByLastNameStartingWith("Smith", page)
  OR->>DB: SELECT ... WHERE last_name LIKE 'Smith%'
  DB-->>OR: Page<Owner>
  alt 1 result
    OR-->>OC: 1 owner
    OC-->>U: redirect /owners/{id}
  else many results
    OR-->>OC: N owners
    OC-->>U: ownersList view
  end
```

## Pet Create (error/recovery)

```mermaid
sequenceDiagram
  participant U as Browser
  participant PC as PetController
  participant V as PetValidator
  participant OR as OwnerRepository
  U->>PC: POST /owners/{id}/pets/new
  PC->>V: validate(pet)
  alt invalid or duplicate name or future birthDate
    V-->>PC: errors
    PC-->>U: redisplay createOrUpdatePetForm
  else valid
    PC->>OR: owner.addPet + save
    OR-->>PC: ok
    PC-->>U: redirect /owners/{id} (flash: added)
  end
```
