**Project Name:** Corporate Dashboard Web Application   
**Current Date for Planning:** May 10, 2025

**Phase 0: Project Initialization & Core Technology Setup**

- [ ] **ID: P0.1** Setup Python development environment (e.g., venv, conda) with a specific Python version (e.g., Python 3.9+).  
- [ ] **ID: P0.2** Initialize Git repository for version control.  
- [ ] **ID: P0.3** **Decision Point:** Select primary Frontend/Dashboarding Framework (e.g., Streamlit, Dash, Panel, Anvil) based on RD Sec 5.1 and "vibe coding" preference. Document rationale.  
- [ ] **ID: P0.4** **Decision Point:** Select Backend Framework (e.g., Flask, FastAPI, Django, or rely on selected dashboarding framework's backend capabilities) if needed, based on RD Sec 5.2. Document rationale.  
- [ ] **ID: P0.5** **Decision Point:** Select Database for application data (PostgreSQL, MySQL) and ORM (SQLAlchemy, Django ORM) based on RD Sec 5.5. Document rationale.  
- [ ] **ID: P0.6** Install core frameworks and libraries identified in P0.3-P0.5.  
- [ ] **ID: P0.7** Create basic project structure (folders for backend, frontend components, tests, configuration, etc.).  
- [ ] **ID: P0.8** Setup configuration management (e.g., `.env` files, config parser) for database credentials, Starburst connection, API keys, etc. (NFR4.6.3).  
- [ ] **ID: P0.9** Establish basic logging mechanism.

**Phase 1: Core Backend Development & Data Models**

- [ ] **ID: P1.1** Design database schema for:  
      - [ ] Users (ID, username, hashed password, email, role, security\_group\_ids)  
      - [ ] SecurityGroups (ID, name)  
      - [ ] UserSecurityGroupMapping (UserID, SecurityGroupID)  
      - [ ] DataSources (ID, name, connection\_details\_for\_starburst\_ref, description, admin\_configured, created\_by\_user\_id)  
      - [ ] Dashboards (ID, name, user\_id, layout\_config\_json, is\_default, created\_at, updated\_at)  
      - [ ] VisualComponents (PBEs) (ID, name, type (chart, map, etc.), data\_source\_id, query\_config, vis\_config\_json, created\_by\_user\_id, global\_share, security\_group\_id\_for\_sharing)  
      - [ ] SharedDashboards (ID, dashboard\_id, shared\_with\_user\_id, shared\_by\_user\_id)  
- [ ] **ID: P1.2** Implement ORM models based on the schema design (RD Sec 5.5).  
- [ ] **ID: P1.3** Create initial database migration scripts.  
- [ ] **ID: P1.4** Develop basic User model with fields for profile information and preferences (RD Sec 3.6.1).  
- [ ] **ID: P1.5** Develop API endpoints (if using a separate backend framework) or backend functions for:  
      - [ ] User registration (if applicable, or user provisioning)  
      - [ ] User login/logout (RD Sec 3.7.1)

**Phase 2: Basic Application Structure & UI Shell**

- [ ] **ID: P2.1** Setup chosen dashboarding framework and create a basic "hello world" application.  
- [ ] **ID: P2.2** Implement the main application layout:  
      - [ ] Header (for app title, user profile access, logout)  
      - [ ] Navigation area (e.g., sidebar for dashboard list, component library access)  
      - [ ] Main content area (for displaying dashboards)  
- [ ] **ID: P2.3** Implement basic routing for different views (e.g., login page, dashboard view, admin section).

**Phase 3: User Role Implementation & Authentication/Authorization**

- [ ] **ID: P3.1** Implement "User" and "Admin" roles in the User model (RD Sec 2.1, 2.2).  
- [ ] **ID: P3.2** Implement secure password hashing and storage.  
- [ ] **ID: P3.3** Integrate chosen authentication library (RD Sec 5.6) for session management or token-based auth (RD Sec 3.7.1).  
- [ ] **ID: P3.4** Implement route protection/decorators to restrict access based on authentication status and user roles (RD Sec 3.7.2).  
- [ ] **ID: P3.5** Create basic UI for login.  
- [ ] **ID: P3.6** Implement Security Group model and User-SecurityGroup mapping (RD Sec 3.6.3, RD Sec 3.7.3).  
- [ ] **ID: P3.7** (Admin) Develop UI for Admins to manage user accounts (create, edit roles, assign to security groups).

**Phase 4: Starburst Integration & Data Source Management (Admin)**

- [ ] **ID: P4.1** Develop a service/module to connect to Starburst Data using selected Python client (PyStarburst, Trino Python client) (RD Sec 3.1.4, RD Sec 5.4).  
      - [ ] Ensure connection parameters are configurable.  
- [ ] **ID: P4.2** (Admin) Implement Admin UI for managing data sources (FR3.1.1, FR3.1.2):  
      - [ ] Form to add new Starburst-virtualized data sources (name, description, relevant Starburst catalog/schema/table info).  
      - [ ] List view of existing data sources with edit/delete options.  
- [ ] **ID: P4.3** (Admin) Implement logic to control visibility/availability of data sources to Users/user groups (FR3.1.3). This may involve linking DataSources to SecurityGroups.  
- [ ] **ID: P4.4** Develop backend functions/API endpoints for Admins to perform CRUD operations on data sources.

**Phase 5: Dashboard Core Functionality (User)**

- [ ] **ID: P5.1** (User) Implement UI for creating a new dashboard (FR3.2.1).  
- [ ] **ID: P5.2** (User) Allow users to name/rename their dashboards (FR3.2.2). Ensure names are unique per user.  
- [ ] **ID: P5.3** (User) Implement functionality to save dashboard configurations (name, layout, component bindings) to the database, associated with the user (FR3.2.5).  
- [ ] **ID: P5.4** (User) Implement functionality to load a user's saved dashboards (FR3.2.7).  
      - [ ] Display a list of user's dashboards in the navigation area.  
- [ ] **ID: P5.5** (User) Implement drag-and-drop interface for dashboard layout (arranging/resizing visual components) using a suitable library (RD Sec 5.7, NFR4.2.2, FR3.2.4).  
      - [ ] Store layout as JSON or similar serializable format.  
- [ ] **ID: P5.6** (User) Implement setting/unsetting a default dashboard (FR3.2.6).  
      - [ ] Application should load the default dashboard on launch for an authenticated user.

**Phase 6: Visual Components & Data Binding (User & Admin)**

- [ ] **ID: P6.1** Integrate chosen Python visualization libraries (Plotly, Bokeh, Altair, etc.) (RD Sec 5.3).  
- [ ] **ID: P6.2** (User) Develop UI for users to add visual components (charts, graphs, maps, tables) to a dashboard (FR3.3.1).  
      - [ ] Provide a selection of component types.  
- [ ] **ID: P6.3** (User) Implement UI for binding an available (authorized) data source to a visual component instance (FR3.3.2).  
      - [ ] This may involve allowing users to specify basic query parameters or select pre-defined views from the data source.  
- [ ] **ID: P6.4** (User) Implement backend logic to fetch data from Starburst based on component's data binding and execute queries.  
- [ ] **ID: P6.5** (User) Implement rendering of data within the visual components.  
- [ ] **ID: P6.6** (User) Implement dynamic updates for visual components (e.g., refresh button, scheduled refresh if feasible) (FR3.3.3).  
- [ ] **ID: P6.7** (User) Allow users to configure basic properties of visual components (title, colors, axes, etc.) (FR3.3.4). Store these configurations.

**Phase 7: Component & Dashboard Libraries (User & Admin)**

- [ ] **ID: P7.1** (Admin) Implement functionality for Admins to create Pre-Bound visual Elements (PBEs) and save them to a global library (FR3.4.6, RD Sec 2.2).  
      - [ ] UI for Admin to select visual component, bind data source, configure, and mark as "globally shared."  
- [ ] **ID: P7.2** (User) Implement functionality for any user to create a PBE (FR3.4.4).  
- [ ] **ID: P7.3** (User) If a non-Admin user creates a PBE, allow them to share it only within their security group(s) (FR3.4.5).  
      - [ ] UI for user to select a security group for sharing their PBE.  
- [ ] **ID: P7.4** Implement a library UI where users can browse/search/filter available PBEs they are authorized to see (global PBEs \+ PBEs shared with their security group) (FR3.4.2, FR3.4.3, FR3.4.7).  
- [ ] **ID: P7.5** (User) Allow users to add PBEs from the library to their current dashboard.  
- [ ] **ID: P7.6** (Admin) Implement functionality for Admins to create and curate a library of pre-configured dashboards (templates) that users can select and customize (FR3.4.1).  
- [ ] **ID: P7.7** (User) Implement UI for users to choose from the library of pre-configured dashboards.

**Phase 8: Dashboard Sharing Functionality (User)**

- [ ] **ID: P8.1** (User) Implement UI for a user to share one of their dashboard configurations with another specific user (by username/email) (FR3.5.1).  
- [ ] **ID: P8.2** Implement backend logic to record dashboard sharing relationships.  
- [ ] **ID: P8.3** When a user accesses a dashboard (their own or shared), ensure data access permissions are enforced based on the *viewing user's* permissions via Starburst (FR3.5.2). This is critical.

**Phase 9: User Profile & Preferences Management**

- [ ] **ID: P9.1** Develop UI for users to view their profile (RD Sec 3.6.1).  
- [ ] **ID: P9.2** Implement saving and loading of user-specific preferences (default dashboard (FR3.2.6), UI theme if applicable) (RD Sec 3.6.2).  
- [ ] **ID: P9.3** Display security group assignments in the user's profile (read-only for User, manageable by Admin) (RD Sec 3.6.3).

**Phase 10: Security, Performance, & Non-Functional Requirements Implementation**

- [ ] **ID: P10.1** Implement CSRF protection for all forms/state-changing requests (NFR4.5.4).  
- [ ] **ID: P10.2** Implement XSS protection (e.g., sanitize user inputs, use secure templating practices) (NFR4.5.4).  
- [ ] **ID: P10.3** Ensure all data in transit is encrypted (HTTPS for web, SSL/TLS for Starburst connection if applicable) (NFR4.5.3). Configure web server for HTTPS.  
- [ ] **ID: P10.4** Conduct performance testing for dashboard loading (NFR4.3.1) and data retrieval (NFR4.3.2).  
- [ ] **ID: P10.5** Optimize database queries and backend logic based on performance testing.  
- [ ] **ID: P10.6** Implement comprehensive error handling and user-friendly error messages.  
- [ ] **ID: P10.7** Review and implement security best practices for the chosen Python frameworks.  
- [ ] **ID: P10.8** Ensure code modularity and add comments/docstrings (NFR4.6.1).

**Phase 11: Testing, Documentation & Deployment Preparation**

- [ ] **ID: P11.1** Write unit tests for backend logic, API endpoints, and critical functions.  
- [ ] **ID: P11.2** Write integration tests for interactions between components (e.g., API and database, Starburst service).  
- [ ] **ID: P11.3** Perform UI testing (manual or automated) to verify all functional requirements.  
- [ ] **ID: P11.4** Create user documentation (how to use features, admin guide).  
- [ ] **ID: P11.5** Create developer documentation (setup, architecture, API docs if applicable).  
- [ ] **ID: P11.6** Prepare deployment scripts/configurations (e.g., Dockerfile, Gunicorn/Uvicorn config).  
- [ ] **ID: P11.7** Conduct User Acceptance Testing (UAT) with representative users and admins.
