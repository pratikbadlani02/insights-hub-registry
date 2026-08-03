# Overview

> Project: spring-petclinic
> Type: rest-api
> Skill: spring-analysis
> Analyzed: 2026-06-28T00:00:00Z

---

## Executive Summary

Spring PetClinic is a **REST/MVC web application** built on **Spring Boot 4.1.0** (`pom.xml:9`) running on **Java 17** (`pom.xml:21`). It manages a veterinary clinic's **owners, pets, visits, and veterinarians**, serving server-rendered **Thymeleaf** pages plus a JSON/XML vet listing. Persistence is via **Spring Data JPA** over an embedded **H2** database by default, with optional **MySQL** and **PostgreSQL** profiles. There is no Kafka, batch, or gateway component — controllers are the sole entry point.

## Core Capabilities

| Capability | Source |
|---|---|
| Owner CRUD + last-name search (paginated) | `owner/OwnerController.java:49` |
| Pet create/edit per owner | `owner/PetController.java:48` |
| Visit booking per pet | `owner/VisitController.java:43` |
| Veterinarian listing (HTML + JSON/XML) | `vet/VetController.java:33` |
| Welcome / home page | `system/WelcomeController.java:24` |
| Exception showcase (`/oups`) | `system/CrashController.java:30` |
| Vet list caching (`vets`) | `vet/VetRepository.java:46` |
| i18n via `?lang=` parameter | `system/WebConfiguration.java:25` |

## Component Count

| Component | Count |
|---|---|
| Controllers | 5 (Owner, Pet, Visit, Vet, Welcome + Crash) |
| Repositories | 3 (Owner, PetType, Vet) |
| JPA entities | 5 (Owner, Pet, Visit, PetType, Vet, Specialty) |
| Config classes | 2 (CacheConfiguration, WebConfiguration) |
| Validators/Formatters | 2 (PetValidator, PetTypeFormatter) |
| Config files | 3 (application + mysql + postgres properties) |

## Service Archetype

**REST/MVC API** — `@Controller` classes are the primary entry point; owns a relational schema; no messaging, batch, or proxy concerns.
