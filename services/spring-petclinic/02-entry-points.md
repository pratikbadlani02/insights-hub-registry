# Entry Points

> Project: spring-petclinic
> Type: rest-api
> Skill: spring-analysis
> Analyzed: 2026-06-28T00:00:00Z

---

### Owners

| Method | Path | Auth | Request | Response | Handler | Description |
|---|---|---|---|---|---|---|
| GET | `/owners/new` | None | — | HTML form | `OwnerController#initCreationForm` | New owner form |
| POST | `/owners/new` | None | Owner form | redirect | `OwnerController#processCreationForm` | Create owner |
| GET | `/owners/find` | None | — | HTML form | `OwnerController#initFindForm` | Search form |
| GET | `/owners` | None | `lastName`, `page` | list/redirect | `OwnerController#processFindForm` | Paginated last-name search |
| GET | `/owners/{ownerId}/edit` | None | — | HTML form | `OwnerController#initUpdateOwnerForm` | Edit form |
| POST | `/owners/{ownerId}/edit` | None | Owner form | redirect | `OwnerController#processUpdateOwnerForm` | Update owner |
| GET | `/owners/{ownerId}` | None | — | HTML detail | `OwnerController#showOwner` | Owner detail |

### Pets

| Method | Path | Auth | Request | Response | Handler | Description |
|---|---|---|---|---|---|---|
| GET | `/owners/{ownerId}/pets/new` | None | — | HTML form | `PetController#initCreationForm` | New pet form |
| POST | `/owners/{ownerId}/pets/new` | None | Pet form | redirect | `PetController#processCreationForm` | Add pet |
| GET | `/owners/{ownerId}/pets/{petId}/edit` | None | — | HTML form | `PetController#initUpdateForm` | Edit pet form |
| POST | `/owners/{ownerId}/pets/{petId}/edit` | None | Pet form | redirect | `PetController#processUpdateForm` | Update pet |

### Visits

| Method | Path | Auth | Request | Response | Handler | Description |
|---|---|---|---|---|---|---|
| GET | `/owners/{ownerId}/pets/{petId}/visits/new` | None | — | HTML form | `VisitController#initNewVisitForm` | New visit form |
| POST | `/owners/{ownerId}/pets/{petId}/visits/new` | None | Visit form | redirect | `VisitController#processNewVisitForm` | Book visit |

### Vets & System

| Method | Path | Auth | Request | Response | Handler | Description |
|---|---|---|---|---|---|---|
| GET | `/vets.html` | None | `page` | HTML list | `VetController#showVetList` | Paginated vet list |
| GET | `/vets` | None | — | JSON/XML | `VetController#showResourcesVetList` | Vet resource list |
| GET | `/` | None | — | HTML | `WelcomeController#welcome` | Home page |
| GET | `/oups` | None | — | error page | `CrashController#triggerException` | Forces exception |

> ⚠️ No authentication or authorization is configured in this codebase. All endpoints are public.

## Actuator / Health

| Endpoint | Purpose |
|---|---|
| `/actuator/health` | Liveness/readiness |
| `/actuator/metrics` | Metrics |
| `/actuator/*` | All exposed (`management.endpoints.web.exposure.include=*`) |
