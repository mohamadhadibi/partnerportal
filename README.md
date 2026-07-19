## 1. Process Overview (Core Understanding)

### User Roles & Workflows

- **Manager :**
    - Created externally by the Vinzenz Group (central entity).
    - Receives an invitation email and logs into the system.
    - **Permissions:**
        - Edit their own profile.
        - Manage specialists within their clinic/organization (add, edit, activate/deactivate).
        - View and manage support tickets submitted by their specialists.

- **Specialist (Partner):**
    - Added to the system by a Manager.
    - Receives an invitation email.
    - Upon first login, completes an initial registration form (profile setup).
    - **State Machine:**
        1. **Pending:** The specialist is registered but awaiting Manager approval.
        2. **Approved/Active:** The Manager reviews and approves the profile. Full access is granted.
        3. **Rejected:** The Manager rejects the profile with a reason provided. The specialist can re-submit with corrected information.
    - **Post-Approval Edits:** Certain critical fields (e.g., qualifications, contact details) trigger a "Needs Review" status when edited. These changes require Manager re-approval before becoming publicly visible.
    - Connect with other partners
    - View blog
    - Update data and manage files.

---

## 2. Technology Stack

| Category | Choice                                                                  |
| :--- |:------------------------------------------------------------------------|
| **Framework** | Flutter (latest stable)                                                 |
| **State Management** | **BLoC** (`flutter_bloc`)                                               |
| **Dependency Injection** | **`get_it`** (service locator)                                          |
| **Routing** | `go_router` (declarative, supports deep linking)                        |
| **Networking** | `dio`                                                                   |
| **Authentication** | **Keycloak**                                                            |
| **Local Storage** | `shared_preferences` (light settings) + `hive` (cache)                  |
| **Error Handling** | `Either` / `Result` pattern (using `dartz` or a custom sealed class)    |
| **Testing** | `flutter_test`, `mockito`, `bloc_test`                                  |
| **Environment Config** | `flutter_config` or `envied` (for keys, URLs, & CI/CD flavor handlings) |

---

## 3. Architecture (Clean Architecture)

We will adopt **Clean Architecture** with three distinct layers:

1. **Presentation Layer:** BLoCs/Cubits, Screens, and Widgets. Consumes use cases and reacts to states.
2. **Domain Layer:** Use cases (interactors), repository interfaces, and entities (plain Dart objects, business logic only).
3. **Data Layer:** Repository implementations, data sources (remote API, local cache), and DTOs (mapped to entities).

### Package Structure (Feature-First)

- auth/ # login, token refresh, role detection
- user/ # partner management: list, add, edit, approve/reject specialists, profile update
- dashboard/ # Home screen with news, quick actions
- tickets/ # Specialist: create/view tickets; Manager: view all tickets, conversation non-realtime
- blog/ # News/articles (list & detail)
- connection/ # Search other specialists, Manage: submit connection requests, remove connection
- files/ # Manage documents (upload/view/download)

Each feature follows the same internal structure:
- `presentation/` (bloc, screens, widgets)
- `domain/` (entities, use cases, repository interfaces)
- `data/` (repository implementations, data sources, models)

---

## 4. Module Breakdown & Estimated Timeline

> **Assumptions:**
> - Team size: **1 full-time developer (solo).**
> - Backend APIs are either ready or developed in parallel.
> - Both minimal/high quality requirements estimated
> - 1 person-day = ~6/7 hours of focused work.

| Module                              | Key Features                                                                                                                                                                                                       | Estimated Effort (Person-Days) |
|:------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------|
| **1. Project Setup & Core**         | Folder structure, DI setup, theming, routing, network client, logging, environment config, base error handling                                                                                                     | 6-12 days                      |
| **2. Authentication**               | Keycloak integration (login, logout, token refresh), role-based navigation, session management, secure storage                                                                                                     | 2-4 days                       |
| **3. Profile Management**           | View/edit own profile (both roles). Specialist: approval status display, submit/update for review on critical fields, handle invitation deep-link flow. Manager: edit personal profile info.                       | 5-8 days                       |
| **4. Partner Management (Manager)** | List of specialists (filterable/searchable). Add new specialist (send invite). Pending approvals list with approve/reject actions (with reason). Show specialist preview, Edit specialist details.                 | 5-14 days                      |
| **5. Dashboard (both)**             | Welcome banner, blog posts, quick shortcuts (new ticket, search, connect). For manager: summary stats (total users, pending tickets).                                                                              | 4-7 days                       |
| **6. Blog / News**                  | List of articles (paginated), detail view, search/filter.                                                                                                                                                          | 2-5 days                       |
| **7. Ticket System**                | Specialist: create ticket (subject, message, category), view own tickets with status. Manager: view all tickets from their clinic, update status/respond. both side can continue sending message on single ticket. | 5-9 days                       |
| **8. Manager Connections**          | Search other specialists (by name, specialty, location, ext). Send connection requests. See list of current connections, submit actions remove/view public profile.                                                | 6-9 days                       |
| **9. File Management**              | List of documents, add/remove/download/view using native file picker.                                                                                                                                              | 2-4 days                       |
| **10. Testing & QA**                | Unit, widget, integration tests; manual QA; bug fixing.                                                                                                                                                            | 2-20 days                      |
| **11. CI/CD & Deployment**          | CI/CD setup, build pipelines for iOS/Android, distribution (TestFlight, Play Store internal), environment switching.                                                                                               | 1-4 days                       |
| **Buffer**                          | Unforeseen issues, UI polish, performance tuning.                                                                                                                                                                  | 5-10 days                      |
| **Total**                           |                                                                                                                                                                                                                    | **~45(min)  ~106(max) days**   |

---

*Prepared for the Vinzenz Group Partner Portal project.*

