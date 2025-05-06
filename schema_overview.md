# Database Schema Overview

## Schema Structure

- **cities**: Stores city information, links to *states*.
- **families**: Family records, linked to *tendas*.
- **masses**: Mass events, linked to *parishes*.
- **parishes**: Parish information, links to *cities* and *states*.
- **priests**: Priests, linked to *users_profiles* and *parishes*.
- **roles**: User roles (devAdmin, Founder, Guardião, etc.).
- **service_roles**: Team/service roles (Líder, Participante, etc.).
- **stages**: Event or tenda stages.
- **states**: State information.
- **system_variables**: Platform configuration.
- **tenda_guardioes**: Tenda guardians, links to *tendas* and *users_profiles*.
- **tendas**: Tenda (group) records, links to *cities*, *states*, *stages*, *parishes*.
- **users_profiles**: User profiles, links to *tendas* and *users_profiles* (spouse).
- **users_service_roles**: User-to-service-role mapping.

## Permissions Overview

| Role      | Read | Insert | Update | Delete | Manage Users | Manage Settings |
|-----------|------|--------|--------|--------|--------------|----------------|
| devAdmin  | ✔️   | ✔️     | ✔️     | ✔️     | ✔️           | ✔️             |
| Founder   | ✔️   | ✔️     | ✔️     | ✔️     | ✔️           | ✔️             |
| Guardião  | ✔️   | (some) | (some) | (no)   | (no)         | (no)           |
| Viewer    | ✔️   | (no)   | (no)   | (no)   | (no)         | (no)           |
| User      | ✔️   | (self) | (self) | (no)   | (no)         | (no)           |
| admin     | ✔️   | ✔️     | ✔️     | ✔️     | (some)       | (some)         |

> **(self):** Only for their own data  
> **(some):** Only for data they are responsible for (e.g., their tenda or team)

## Entity Relationship Diagram (ERD)

![Database Schema Diagram](database_schema.svg)

> If the diagram does not display, open `database_schema.svg` directly in your browser. 