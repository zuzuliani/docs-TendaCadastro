# Database Documentation

## Overview
This document provides a comprehensive overview of the database schema, including tables, relationships, and security policies.

## Schema Organization
The database is organized into several schemas:
- `auth`: Authentication and user management
- `public`: Main application data
- `storage`: File storage management
- `realtime`: Real-time messaging
- `vault`: Secrets management

## Tables

### Public Schema

#### cities
- **Primary Key**: `id`
- **Foreign Keys**:
  - `state_id` references `states(id)`
- **RLS Policies**:
  - `cities_devadmin_all_access`: Full access for devAdmin role
  - `cities_founder_all_access`: Full access for Founder role
  - `cities_guardiao_read`: Read access for guardiao role
  - `cities_user_read`: Read access for authenticated users
  - `cities_viewer_read`: Read access for viewers

#### families
- **Primary Key**: `id`
- **Foreign Keys**:
  - `tenda_id` references `tendas(id)`
- **RLS Policies**:
  - `families_devadmin_all_access`: Full access for devAdmin role
  - `families_founder_all_access`: Full access for Founder role
  - `families_user_read`: Read access for authenticated users
  - `families_viewer_read`: Read access for viewers

#### masses
- **Primary Key**: `id`
- **Foreign Keys**:
  - `parish_id` references `parishes(id)`
- **RLS Policies**:
  - `masses_devadmin_all_access`: Full access for devAdmin role
  - `masses_founder_all_access`: Full access for Founder role
  - `masses_user_read`: Read access for authenticated users
  - `Enable insert for authenticated users only`: Full access for authenticated users

#### parishes
- **Primary Key**: `id`
- **RLS Policies**:
  - `parishes_devadmin_all_access`: Full access for devAdmin role
  - `parishes_founder_all_access`: Full access for Founder role
  - `parishes_guardiao_read`: Read access for guardiao role
  - `parishes_user_read`: Read access for authenticated users
  - `parishes_viewer_read`: Read access for viewers

#### priests
- **Primary Key**: `id`
- **Foreign Keys**:
  - `profile_id` references `users_profiles(id)`
  - `parish_id` references `parishes(id)`
- **RLS Policies**:
  - `priests_devadmin_all_access`: Full access for devAdmin role
  - `priests_founder_all_access`: Full access for Founder role
  - `priests_user_read`: Read access for authenticated users
  - `priests_viewer_read`: Read access for viewers

#### tendas
- **Primary Key**: `id`
- **Foreign Keys**:
  - `city_id` references `cities(id)`
  - `state_id` references `states(id)`
  - `stage_id` references `stages(id)`
  - `parish_id` references `parishes(id)`
- **RLS Policies**:
  - `tendas_devadmin_all_access`: Full access for devAdmin role
  - `tendas_founder_all_access`: Full access for Founder role
  - `tendas_guardiao_read`: Read access for guardiao role
  - `tendas_user_read`: Read access for authenticated users
  - `tendas_viewer_read`: Read access for viewers

#### users_profiles
- **Primary Key**: `id`
- **Foreign Keys**:
  - `tenda_id` references `tendas(id)`
  - `spouse_id` references `users_profiles(id)`
- **RLS Policies**:
  - `users_profiles_devadmin_all_access`: Full access for devAdmin role
  - `users_profiles_founder_all_access`: Full access for Founder role
  - `users_profiles_guardiao_read`: Read access for guardiao role
  - `users_profiles_self_update`: Users can update their own profiles
  - `users_profiles_user_read`: Read access for authenticated users
  - `users_profiles_viewer_read`: Read access for viewers

### Storage Schema

#### objects
- **Primary Key**: `id`
- **Foreign Keys**:
  - `bucket_id` references `buckets(id)`
- **RLS Policies**:
  - `Allow anyone to upload family pictures`: Public insert access for family pictures
  - `Allow authenticated users to view family pictures`: Authenticated users can view family pictures
  - `Only devAdmin can delete family pictures`: Only devAdmin can delete family pictures
  - `Only devAdmin can update family pictures`: Only devAdmin can update family pictures

#### states
- **Primary Key**: `id`
- **RLS Policies**:
  - `devadmin_all_access`: Full access for devAdmin role
  - `states_user_read`: Read access for authenticated users

#### stages
- **Primary Key**: `id`
- **RLS Policies**:
  - `stages_devadmin_all_access`: Full access for devAdmin role
  - `stages_founder_all_access`: Full access for Founder role
  - `stages_guardiao_read`: Read access for guardiao role
  - `stages_user_read`: Read access for authenticated users
  - `stages_viewer_read`: Read access for viewers

#### tenda_guardioes
- **Primary Key**: `id`
- **Foreign Keys**:
  - `tenda_id` references `tendas(id)`
  - `profile_id` references `users_profiles(id)`
- **RLS Policies**:
  - `tenda_guardioes_devadmin_all_access`: Full access for devAdmin role
  - `tenda_guardioes_founder_all_access`: Full access for Founder role

## Security

### Row Level Security (RLS)
All tables in the database have RLS enabled, but none have forced RLS. This means that:
- RLS policies are active
- Users can bypass RLS if they have the appropriate permissions

### Role-Based Access Control
The system implements several roles:
- `devAdmin`: Full access to all tables
- `Founder`: Full access to all tables
- `authenticated`: Basic read access to most tables
- `service_role`: Special role for service operations
- Various team leader roles (e.g., `Líder de Equipe Ventania`, `Líder de Equipe Tsedaka`)

### Service Roles
The system includes several service roles for team management:
- Líder de Equipe Ventania
- Líder de Equipe Tsedaka
- Líder de Equipe GAA
- Líder de Equipe Berçário/Creche
- Líder de Equipe Consagrados
- Treinador de Equipe de Trabalho

### Roles and Permissions

The platform uses a role-based access control (RBAC) system. Each user is assigned one or more roles, which determine their permissions throughout the application. Below are the main roles and their typical permissions:

#### 1. devAdmin
- **Description:** Developer Administrator. This is the highest privilege role, intended for technical administrators.
- **Permissions:**
  - Full access (read, insert, update, delete) to all tables and data.
  - Can manage users, roles, and all application settings.
  - Can bypass most RLS restrictions via explicit policies.

#### 2. Founder
- **Description:** Founding member or super-admin.
- **Permissions:**
  - Full access (read, insert, update, delete) to all tables and data.
  - Can manage users and high-level application settings.
  - Similar privileges to devAdmin, but may be reserved for non-technical founders.

#### 3. Guardião
- **Description:** Guardian or group leader.
- **Permissions:**
  - Read access to most tables (e.g., cities, parishes, priests, tendas, users_profiles).
  - May have additional permissions to manage or view data related to their group or tenda.
  - Cannot perform destructive actions (insert, update, delete) unless explicitly granted.

#### 4. Viewer
- **Description:** Read-only user.
- **Permissions:**
  - Can view public data (e.g., cities, families, parishes, priests, tendas, users_profiles).
  - Cannot modify any data.

#### 5. User
- **Description:** Regular authenticated user.
- **Permissions:**
  - Can view most data relevant to the community (e.g., contact info, tendas, events).
  - Can update their own profile.
  - Cannot modify or delete other users' data.

#### 6. admin
- **Description:** General administrator (may be used for legacy or specific admin tasks).
- **Permissions:**
  - Permissions may overlap with devAdmin or Founder, but typically more restricted.
  - Can manage some data and users, depending on RLS policies.

---

#### How Permissions Are Enforced

- **Row Level Security (RLS):** Most permissions are enforced at the database level using RLS policies. For example, only devAdmin and Founder can perform all actions on sensitive tables, while other roles are limited to read-only or self-management.
- **Service Roles:** There are also service roles (e.g., team leaders) defined in the `service_roles` table, which grant permissions for managing specific teams or services.

---

#### Example Policy Mapping

| Role      | Read | Insert | Update | Delete | Manage Users | Manage Settings |
|-----------|------|--------|--------|--------|--------------|----------------|
| devAdmin  | ✔️   | ✔️     | ✔️     | ✔️     | ✔️           | ✔️             |
| Founder   | ✔️   | ✔️     | ✔️     | ✔️     | ✔️           | ✔️             |
| Guardião  | ✔️   | (some) | (some) | (no)   | (no)         | (no)           |
| Viewer    | ✔️   | (no)   | (no)   | (no)   | (no)         | (no)           |
| User      | ✔️   | (self) | (self) | (no)   | (no)         | (no)           |
| admin     | ✔️   | ✔️     | ✔️     | ✔️     | (some)       | (some)         |

> (self): Only for their own data  
> (some): Only for data they are responsible for (e.g., their tenda or team)

## Notes
- All tables in the `auth` schema are managed by Supabase Auth
- The `storage` schema is used for file storage, with specific policies for family pictures
- The `realtime` schema handles real-time messaging functionality
- The `vault` schema is used for secrets management 

## Next Steps: Service Roles Integration

Currently, service roles (such as team leaders and other special roles defined in the `service_roles` table) have not yet been integrated into the Row Level Security (RLS) policies. Implementing RLS policies that leverage these service roles will allow for more granular and flexible access control, especially for team-based or service-specific permissions.

**Recommended next steps:**
- Analyze the `service_roles` table and its relationships to users and data.
- Define which tables and actions should be governed by service roles (e.g., allowing team leaders to manage only their team's data).
- Implement RLS policies that check for service role membership, similar to how user roles are currently checked.
- Test and document the new policies to ensure they meet the application's security and business requirements.

### Service Roles and Potential Permissions
Below is a list of current service roles and a simple description of the potential permissions each could have:

- **Líder de Equipe Consagrados**: Manage and view data for the Consagrados team; approve or update team member information.
- **Líder de Equipe Tsedaka**: Manage and view data for the Tsedaka team; approve or update team member information.
- **Padre Paroquial**: View and manage parish-related data; oversee parish events and members.
- **Fundador**: Platform-wide permissions, similar to super-admin; oversee all teams and data.
- **Participante de Equipe Berçário/Creche**: View and participate in Berçário/Creche team activities; limited edit permissions.
- **Participante de Equipe Ventania**: View and participate in Ventania team activities; limited edit permissions.
- **Líder de Equipe Berçário/Creche**: Manage and view data for the Berçário/Creche team; approve or update team member information.
- **Líder de Equipe GAA**: Manage and view data for the GAA team; approve or update team member information.
- **Guardião**: Oversee and manage a group or tenda; view and update group data.
- **Cofundador**: Platform-wide permissions, similar to Fundador; oversee all teams and data.
- **Padre**: View and manage parishioner and event data; limited to parish scope.
- **Participante de Equipe de Trabalho**: View and participate in Equipe de Trabalho activities; limited edit permissions.
- **Treinador de Equipe de Trabalho**: Manage and view data for Equipe de Trabalho; oversee training and team development.

These descriptions are suggestions and should be refined as you define your access control requirements. Integrating these service roles into RLS will allow for more precise and flexible permissions management across your platform. 