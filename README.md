## 1. Core Understanding

- **Specialist (Partner):**
    - profile complete
    - data and file
    - connections
    - blog
- **Manager :**
    - profile edit
    - manage partners
    - tickets
    - plus all partner accesses

---

## 2. Technology Stack

| Category | Choice                                                                  |
| :--- |:------------------------------------------------------------------------|
| **Architecture** | Clean Architecture                                                 |
| **State Management** | **BLoC** (`flutter_bloc`)                                               |
| **Dependency Injection** | **`get_it`** (service locator)                                          |
| **Routing** | `go_router` (declarative, supports deep linking)                        |
| **Networking** | `dio`                                                                   |
| **Authentication** | **Keycloak**                                                            |
| **Local Storage** | `shared_preferences` (light settings) + `hive` (cache)                  |
| **Error Handling** | `Either` / `Result` pattern (using `dartz` or a custom sealed class)    |

---

## 3. Module Breakdown & Estimated Timeline

> **Assumptions:**
> - Team size: **1 full-time developer (solo).**
> - Backend APIs are either ready or developed in parallel.
> - Estimate for both minimum/maximum requirements 
> - 1 person-day = ~6/7 hours of focused work.

| Module                              | Key Features                                                                                                                                                                                                       | Estimated Effort (Person-Days) |
|:------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------|
| **1. Project Setup & Core**         | Folder structure, DI setup, theming, routing, network client, logging, environment config, base error handling                                                                                                     | 5-7 days                       |
| **2. Authentication**               | Keycloak integration (login, logout, token refresh), role-based navigation, session management, secure storage                                                                                                     | 2-3 days                       |
| **3. Profile Management**           | View/edit own profile (both roles). Specialist: approval status display, submit/update for review on critical fields, handle invitation deep-link flow. Manager: edit personal profile info.                       | 5-8 days                       |
| **4. Partner Management (Manager)** | List of specialists (filterable/searchable). Add new specialist (send invite). Pending approvals list with approve/reject actions (with reason). Show specialist preview, Edit specialist details.                 | 2-4 days                       |
| **5. Dashboard (both)**             | Welcome banner, blog posts, quick shortcuts (new ticket, search, connect). For manager: summary stats (total users, pending tickets).                                                                              | 3-5 days                       |
| **6. Blog / News**                  | List of articles (paginated), detail view, search/filter.                                                                                                                                                          | 2-4 days                       |
| **7. Ticket System**                | Specialist: create ticket (subject, message, category), view own tickets with status. Manager: view all tickets from their clinic, update status/respond. both side can continue sending message on single ticket. | 3-5 days                       |
| **8. Manager Connections**          | Search other specialists (by name, specialty, location, ext). Send connection requests. See list of current connections, submit actions remove/view public profile.                                                | 4-5 days                       |
| **9. File Management**              | List of documents, add/remove/download/view using native file picker.                                                                                                                                              | 1-3 days                       |
| **11. CI/CD & Deployment**          | CI/CD setup, build pipelines for iOS/Android, distribution (TestFlight, Play Store internal), environment switching.                                                                                               | 1-4 days                       |
| **Total**                           |                                                                                                                                                                                                                    | **~28(min)  ~48(max) days**    |



