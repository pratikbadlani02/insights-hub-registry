# Data Model

> Project: spring-petclinic1
> Type: rest-api
> Skill: spring-analysis
> Analyzed: 2026-06-28T00:00:00Z

---

## Core Entities (JPA)

```
@MappedSuperclass BaseEntity { @Id @GeneratedValue Integer id }
@MappedSuperclass NamedEntity extends BaseEntity { String name }
@MappedSuperclass Person extends BaseEntity { String firstName; String lastName }

@Entity @Table("owners") Owner extends Person {
  String address; String city; String telephone  // \d{10}
  @OneToMany(EAGER) List<Pet> pets  // joinColumn owner_id
}
@Entity @Table("pets") Pet extends NamedEntity {
  LocalDate birthDate
  @ManyToOne PetType type            // type_id
  @OneToMany(EAGER) Set<Visit> visits  // pet_id
}
@Entity @Table("visits") Visit extends BaseEntity { LocalDate date; String description }
@Entity @Table("types") PetType extends NamedEntity {}
@Entity @Table("vets") Vet extends Person {
  @ManyToMany Set<Specialty> specialties  // vet_specialties
}
@Entity @Table("specialties") Specialty extends NamedEntity {}
```

## Database Schema (`db/h2/schema.sql`)

| Table | Primary Key | Foreign Keys | Indexes |
|---|---|---|---|
| owners | id | — | owners_last_name |
| pets | id | owner_id→owners, type_id→types | pets_name |
| types | id | — | types_name |
| visits | id | pet_id→pets | visits_pet_id |
| vets | id | — | vets_last_name |
| specialties | id | — | specialties_name |
| vet_specialties | (vet_id, specialty_id) | vet_id→vets, specialty_id→specialties | — |

## DTOs

- `Vets` — XML/JSON wrapper of `List<Vet>` for `/vets` (`vet/Vets.java`). No other DTOs; controllers bind directly to entities.
