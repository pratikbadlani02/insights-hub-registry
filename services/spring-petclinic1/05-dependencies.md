# Dependencies

> Project: spring-petclinic1
> Type: rest-api
> Skill: spring-analysis
> Analyzed: 2026-06-28T00:00:00Z

---

## Service Call Graph

| From | To | Method | Protocol | Purpose |
|---|---|---|---|---|
| Browser | PetClinic | HTTP | HTTP | Owner/Pet/Visit/Vet pages |
| Controllers | OwnerRepository | JPA | JDBC | Owner/Pet/Visit persistence |
| Controllers | VetRepository | JPA | JDBC | Vet listing (cached) |
| Controllers | PetTypeRepository | JPA | JDBC | Pet type lookup |

> No downstream REST clients, Kafka, or external services in source. N/A for inter-service URLs.

## Data Stores

### Relational database
| Repository | Tables | Key queries |
|---|---|---|
| OwnerRepository | owners, pets, visits | `findByLastNameStartingWith`, `findById` |
| PetTypeRepository | types | `findPetTypes` (ORDER BY name) |
| VetRepository | vets, specialties | `findAll` cached as `vets` |

Connection: H2 embedded by default; MySQL/PostgreSQL via JDBC URL env vars (see deployment).

## Kafka Integration

**None.** No Kafka producers or consumers.

## Cache

| Cache | Provider | Where |
|---|---|---|
| `vets` | Caffeine via JCache | `VetRepository#findAll` (`@Cacheable`), config `system/CacheConfiguration.java` |

## HTTP Client

N/A — no RestTemplate/WebClient/Feign; this service makes no outbound HTTP calls.
