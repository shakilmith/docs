## Important annotations to create jpa entity

1. @Entity - make the class persistent class
2. @Table - optional table name
3. @Id - make the id primary key
4. @GeneratedValue - auto generate id
5. @Column - optional column name
6. @Transient - it exclude a field from persistent
7. @Lob - for large objects (BLOB or CLOB)
8. @Enumerated - for mapping enums
9. @Temporal - for legacy Date
10. Relationships annotations:
    - OneToOne
    - OneToMany
    - ManyToOne
    - ManyToMany
    - @JoinColumn
    - @JoinTable
    - @MapsId
    - @Inheritance
    - @DiscriminatorColumn(name = "type")
    - @DiscriminatorValue("ADMIN")
11. @Embeddable - for embedded objects
12. @Embedded
13. @AttributeOverride - for changing the attribute name (in database tables)
14. Lifecycle Callback Annotations:
    - @PrePersist
    - @PostPersist
    - @PreUpdate
    - @PostUpdate
    - @PreRemove
    - @PostRemove
    - @PostLoad
    - @PrePersist
    public void beforeSave() { }

15. Fetching & Cascading:
    - FetchType.LAZY / FetchType.EAGER
    - CascadeType.ALL, PERSIST, MERGE, REMOVE
16. @Version
17. @NamedQuery
18. @NamedNativeQuery
19. @SecondaryTable
20. @ElementCollection
21. @Inheritance


