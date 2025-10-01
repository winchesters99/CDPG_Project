# Spring Boot Keycloak Tree Path & Partition Service

This is a sample Spring Boot application for CDPG project:

1. **Finding paths in a binary tree** using a parent provider.
2. **Partitioning weights into two buckets** to minimize difference .
3. **Keycloak OIDC integration** with JWT authentication and role-based authorization.

---

## Features

- **Tree Path Finder** (`/api/path`)  
  Given a source and destination node, returns the path between them.

- **Partition Solver** (`/api/partition/exact` and `/api/partition/dp`)  
  - Exact partition (admin only, brute-force for small N)  
  - Dynamic programming partition (efficient for larger N)  

- **Security**  
  - OAuth2 Resource Server with JWT (Keycloak)  
  - `@PreAuthorize` method-level security for admin-only endpoints  
  - Roles extracted from Keycloak `realm_access` and `resource_access`.


## Requirements

- Java 17+
- Maven 3.8+
- Keycloak Server running with a realm and client configured

---

## Setup Keycloak

1. **Create Realm**  
   - Example: `myrealm`

2. **Create Client**  
   - Client ID: `tree-service`
   - Access Type: `bearer-only` (no login page)
   - Valid Redirect URIs: leave blank for resource server

3. **Create Roles**  
   - Realm role: `admin` (for testing `/partition/exact` endpoint)
   - Optionally create client roles and assign them to users

4. **Create Users**  
   - Assign `admin` role to a test user  
   - Export Keycloak realm public key or use JWK URL

5. **Configure `application.properties`**  

```properties
spring.security.oauth2.resourceserver.jwt.jwk-set-uri=https://<KEYCLOAK_HOST>/realms/<REALM>/protocol/openid-connect/certs
server.port=8080
Replace <KEYCLOAK_HOST> and <REALM> with your Keycloak server and realm name.


Run the project with mvn clean install

The service will start at http://localhost:8080.
