## H2 database configuration for spring boot project

```
## For H2 database configuration
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect


#enabling the H2 console
spring.h2.console.enabled=true

# in order to work with data.sql file 
spring.jpa.defer-datasource-initialization=true

## when you work with mysql or postgresql and want to load data from data.sql file
spring.sql.init.mode=always
```