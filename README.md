Community Event Tool
====================

A web application to streamline event planning and decision-making for large friend groups or communities. Users can create themed groups, propose events, and collaboratively organize activities through voting and discussion.

Status: In Development - Building Locally

Current Phase
-------------
🚧 **Active Development** - Building core features locally with H2 database
- Focus: Local development until app reaches near-completion
- Database: H2 in-memory (auto-configured, no setup needed)
- Deployment: Planned for later (Render + Supabase for free hosting)

Overview
--------
This app helps communities decide what to do and when by combining proposals, votes, discussion, and scheduling into one place.

Core Features
-------------
- Group-based organization with customizable themes (e.g., "This Week's Activities", "Birthday Parties", "Outdoor Adventures").
- Event proposals with details, dates, locations, tags, and attachments.
- Democratic voting with upvote/downvote (and optional neutral) plus closing deadlines.
- Real-time discussion threads per proposal with live notifications.
- Centralized calendar for confirmed events, deadlines, and milestones.
- Member availability tracking and automated scheduling conflict detection.

Tech Stack
----------
- **Backend**: Java 21 LTS + Spring Boot 3.x + Spring Data JPA
- **Frontend**: Angular 17 + TypeScript
- **Build Tools**: Maven (backend), npm (frontend)
- **Database**: PostgreSQL (production), H2 (local dev/testing)
- **Testing**: JUnit 5 + Mockito (backend), Jasmine/Karma or Jest (frontend)
- **Real-time**: WebSocket (Spring WebSocket + STOMP)
- **Auth**: Spring Security + JWT or OAuth2 (Google/Discord)

High-Level Architecture
------------------------
- **Frontend**: Angular SPA with routing, reactive forms, and real-time event updates via WebSocket.
- **Backend**: RESTful API + WebSocket endpoints. Spring Boot with JPA entities, repositories, services, and controllers.
- **Database**: Relational schema (PostgreSQL in production; H2 for rapid local dev). Event- and group-centric design.
- **Notifications**: WebSocket push for live updates; background jobs (Spring @Scheduled) for deadline processing.
- **Auth**: Role-based permissions per group. JWT tokens or Spring OAuth2 integration.

Getting Started
---------------
1) **Prerequisites**
   - Java 21 LTS 
   - Maven 3.9+ 
   - Node.js LTS
   - npm
   - Angular CLI 17+

2) **Setup**
   ```powershell
   # Backend (Spring Boot)
   cd backend
   mvn clean install
   mvn spring-boot:run
   # Runs on http://localhost:8080
   # H2 console: http://localhost:8080/h2-console (JDBC URL: jdbc:h2:mem:testdb, user: sa, password: blank)
   
   # Frontend (Angular) - in a new terminal
   cd frontend
   npm install
   npm start
   # Runs on http://localhost:4200
   ```

3) **Run Tests**
   ```powershell
   # Backend tests (JUnit)
   cd backend
   mvn test
   
   # Frontend tests (Jasmine/Karma)
   cd frontend
   npm test
   ```

**Current Development Setup:**
- Using H2 in-memory database (data resets on restart - perfect for rapid development)
- No database installation required
- No external services needed
- Fast feedback loop for development

Project Structure
-----------------
```
community-event-tool/
├── backend/              # Spring Boot application
│   ├── src/
│   │   ├── main/java/    # Application code
│   │   │   └── CommunityEventApplication.java
│   │   ├── main/resources/ # application.yml, static files
│   │   └── test/java/    # JUnit tests
│   └── pom.xml
├── frontend/             # Angular application
│   ├── src/
│   │   ├── app/          # Components, services, models
│   │   └── assets/       # Images, styles
│   ├── angular.json
│   ├── package.json
│   └── tsconfig.json
├── .gitignore
└── README.md
```

**Testing Strategy:**
- Backend: JUnit 5 tests in `backend/src/test/java/` (unit + integration tests with `@SpringBootTest`)
- Frontend: Jasmine/Karma (default) or Jest in `frontend/src/app/**/*.spec.ts`
- Both stacks have separate test runners and can be executed independently

Data Model Sketch (first pass)
------------------------------
- User: id, name, email, avatarUrl, timezone
- Group: id, name, theme, description, createdBy, visibility (private/invite/public)
- GroupMember: groupId, userId, role (owner, admin, member)
- EventProposal: id, groupId, title, description, location, proposedBy, proposedDates[], tags[], status (open, scheduled, closed)
- Vote: id, proposalId, userId, value (+1/-1)
- Comment: id, proposalId, userId, body, createdAt, parentId?
- Availability: id, userId, proposalId or eventId, timeslot, status (available/maybe/unavailable)
- Event (confirmed): id, groupId, title, dateTime, location, createdFromProposalId

Deployment
----------
**Note:** Deployment is planned for after core features are complete.

**Planned: Free hosting (when ready to deploy) due to not needing much**
- **Frontend + Backend:** Render (free tier)
- **Database:** Supabase PostgreSQL (free forever, 500MB)

Roadmap
-------
**Phase 1: Core Backend (Current)**
- ✅ Project structure and build setup
- [ ] Database entities (User, Group, EventProposal, Vote, Comment)
- [ ] JPA repositories and service layer
- [ ] REST API endpoints (CRUD operations)
- [ ] Basic validation and error handling

**Phase 2: Core Frontend**
- [ ] Angular routing and navigation
- [ ] Group management UI
- [ ] Event proposal creation and listing
- [ ] Voting interface
- [ ] Basic styling and responsive design

**Phase 3: Advanced Features**
- [ ] Spring Security + JWT authentication
- [ ] Real-time updates (WebSocket/STOMP)
- [ ] Comment threads and notifications
- [ ] Calendar view integration
- [ ] Availability tracking and conflict detection

**Phase 4: Polish & Deploy**
- [ ] Comprehensive testing (unit + integration + e2e)
- [ ] Admin and moderation tools
- [ ] Accessibility improvements
- [ ] Performance optimization
- [ ] Deploy to Render + Supabase

License
-------
TBD

