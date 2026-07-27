# Error Handling

> Project: spring-petclinic1
> Type: rest-api
> Skill: spring-analysis
> Analyzed: 2026-06-28T00:00:00Z

---

### Success Codes
| Code | When |
|---|---|
| 200 | Page render |
| 302 | Redirect after create/update/save |

### Client Error Codes
| Code | When |
|---|---|
| 400 | Bean validation failure on bound entity |
| 404 | Unknown route |

### Server Error Codes
| Code | When |
|---|---|
| 500 | Unhandled `RuntimeException` (e.g. `/oups`, unknown owner id) → `error.html` |

## Exception Flow

```
IllegalArgumentException (owner/pet not found) ── thrown in controllers
RuntimeException ────────────────────────────── /oups showcase
                 └── resolved to error.html view
```

## Validation Handling

- Form errors collected in `BindingResult`; controllers redisplay the form with field rejections (`OwnerController`, `PetController`, `VisitController`).
- `@ControllerAdvice` — N/A: none defined; default Spring Boot error page handles uncaught exceptions.

## Transactional Boundaries

- `VetRepository.findAll` annotated `@Transactional(readOnly = true)`. Other writes use repository `save` within the default request transaction.
