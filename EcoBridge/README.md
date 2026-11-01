# EcoBridge

EcoBridge is a full-stack environmental community platform for scheduling recyclable-waste pickups, joining local eco events, sharing community activities, and managing verified collectors.

**Live website:** [https://ecobridge-delta.vercel.app](https://ecobridge-delta.vercel.app)  
**Project repository:** [https://github.com/shresthakosanam/EcoBridge](https://github.com/shresthakosanam/EcoBridge)  
**MRU CSE Second Year Projects:** [https://github.com/cse-department-projects/MRU-CSE-2nd-Year-Projects](https://github.com/cse-department-projects/MRU-CSE-2nd-Year-Projects)

## Main features

- Email/password signup and login with BCrypt password hashing
- Persistent PostgreSQL-backed login sessions
- Doorstep recycling pickup requests and status tracking
- Collector application, administrator approval, and collector portal
- Eco-event creation and registration
- Community feed with posts, likes, comments, and image uploads
- Member dashboard, profile, and collective-impact statistics
- Administrator dashboard for users, collectors, pickups, events, and posts
- Responsive frontend for desktop and mobile devices

## Technology stack

- Java 21
- Spring Boot 3.5.4
- Spring Security and Spring Session JDBC
- Spring Data JPA and Hibernate
- PostgreSQL on Supabase
- Flyway database migrations
- HTML, CSS, and vanilla JavaScript
- Maven
- Docker and Vercel Services
- Firebase Admin SDK for optional image storage

## Project structure

```text
src/main/java/com/ecobridge/       Spring Boot application code
src/main/resources/static/        Website pages, CSS, and JavaScript
src/main/resources/db/migration/  MySQL and PostgreSQL migrations
src/test/                         Automated tests
database/                         Local database setup resources
Dockerfile                        Production container build
vercel.json                       Vercel Services configuration
pom.xml                           Maven dependencies and build configuration
```

## Run locally

### Requirements

- Java 21 or newer
- Maven 3.9 or newer

The default local profile uses an embedded H2 database, so Supabase is not required for a basic local demonstration.

```bash
mvn clean package
java -jar target/ecobridge-1.0.0.jar
```

Open [http://localhost:8080](http://localhost:8080).

On Windows, `start-ecobridge.ps1` can also start the local application.

## Supabase configuration

For PostgreSQL, copy `.env.example` to the ignored `.env.local` file and provide these values from the Supabase **Connect** panel:

```env
SPRING_PROFILES_ACTIVE=supabase
SUPABASE_DB_URL=jdbc:postgresql://your-pooler-host:5432/postgres?sslmode=require
SUPABASE_DB_USERNAME=postgres.your-project-reference
SUPABASE_DB_PASSWORD=your-private-database-password
```

The `supabase` profile runs migrations from `src/main/resources/db/migration/postgresql`. Login sessions are stored in PostgreSQL so authentication remains valid across multiple deployed containers.

## Vercel deployment

EcoBridge runs as a Java container using Vercel Services. Configure the Supabase variables above for Production and Preview, then deploy the repository. The `Dockerfile` and `vercel.json` files contain the required container and routing configuration.

## Security

- Passwords are stored only as BCrypt hashes.
- Production database credentials are environment variables and are not committed.
- Session cookies are HTTP-only, Secure, and SameSite=Lax.
- Supabase tables use Row Level Security to block direct anonymous Data API access.
- Firebase service-account JSON and `.env.*` files are excluded from Git.

Never commit a real database password, Firebase private key, `.env.local`, or service-account JSON file.

## Testing

```bash
mvn test
```

The automated suite covers authentication, session continuity, administrator collector approval, and database-backed image fallback behavior.

## Submission note

This project is prepared for submission to the [MRU-CSE-2nd-Year-Projects](https://github.com/cse-department-projects/MRU-CSE-2nd-Year-Projects) repository. Upload the extracted `EcoBridge` folder or submit it through a fork and pull request, depending on the department repository's contribution process.

## Author

Shreshta Kosanam
