# Deployment

> Project: spring-petclinic1
> Type: rest-api
> Skill: spring-analysis
> Analyzed: 2026-06-28T00:00:00Z

---

## Build & Run

```bash
./mvnw package
java -jar target/*.jar
# image build (Cloud Native Buildpacks)
./mvnw spring-boot:build-image
```

> No Dockerfile in repo; container image is produced by `spring-boot-maven-plugin` build-image (`pom.xml:408`). `docker-compose.yml` provides MySQL/PostgreSQL.

## Configuration by Profile

| Profile | Database | JDBC URL default | Init mode |
|---|---|---|---|
| default | H2 | embedded | schema+data.sql |
| mysql | MySQL | `jdbc:mysql://localhost/petclinic` | always |
| postgres | PostgreSQL | `jdbc:postgresql://localhost/petclinic` | always |

## Environment Variables

| Variable | Default | Purpose |
|---|---|---|
| MYSQL_URL | `jdbc:mysql://localhost/petclinic` | MySQL JDBC URL |
| MYSQL_USER | petclinic | MySQL user |
| MYSQL_PASS | petclinic | MySQL password |
| POSTGRES_URL | `jdbc:postgresql://localhost/petclinic` | Postgres JDBC URL |
| POSTGRES_USER | petclinic | Postgres user |
| POSTGRES_PASS | petclinic | Postgres password |

## Actuator / Health

| Endpoint | Purpose |
|---|---|
| `/actuator/health` | Health |
| `/actuator/metrics` | Metrics |
| `/actuator/*` | All exposed (dev only) |

## Notes

- `spring.jpa.hibernate.ddl-auto=none`; schema seeded from `db/${database}/schema.sql` + `data.sql`.
- Static resources cached 12h (`spring.web.resources.cache.cachecontrol.max-age=12h`).
