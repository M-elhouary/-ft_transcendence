# Architecture decisions

## ADR-001: Use React and TypeScript for the frontend

### Decision

The frontend will use React with TypeScript.

### Responsibilities

The frontend is responsible for:

- Rendering pages and components
- User interaction
- Client-side routing
- Form handling
- Calling the backend API
- Displaying loading, empty, success, and error states
- Managing the client-side chat connection
- Managing local UI state

### Rules

- Frontend code must not make authorization decisions.
- Frontend validation improves user experience but does not replace backend validation.
- Shared request and response types should be reused where practical.
- Components should be organized by feature.
- API calls should use a shared API client instead of direct requests scattered across components.

### Recommended frontend structure

```text
apps/web/
├── src/
│   ├── app/
│   │   ├── App.tsx
│   │   ├── routes.tsx
│   │   └── providers.tsx
│   ├── components/
│   │   ├── ui/
│   │   ├── forms/
│   │   └── feedback/
│   ├── features/
│   │   ├── auth/
│   │   ├── student/
│   │   ├── company/
│   │   ├── opportunities/
│   │   ├── submissions/
│   │   ├── preparation/
│   │   ├── invitations/
│   │   └── chat/
│   ├── layouts/
│   ├── pages/
│   ├── services/
│   │   └── api-client.ts
│   ├── hooks/
│   ├── lib/
│   ├── types/
│   └── main.tsx
├── package.json
├── tsconfig.json
└── vite.config.ts
```

## ADR-002: Use Node.js, Express, and TypeScript for the backend

### Decision

The backend will run on Node.js, use Express as its HTTP framework, and be written in TypeScript.

```text
Node.js = runtime
Express = HTTP/API framework
TypeScript = programming language
```

### Responsibilities

The backend is responsible for:

- REST API endpoints
- Authentication
- Authorization
- Input validation
- Business workflows
- Database access
- File access control
- Notifications
- Chat authorization and messaging
- Health checks
- Logging
- Metrics

### Recommended backend structure

```text
apps/api/
├── src/
│   ├── app.ts
│   ├── server.ts
│   ├── config/
│   ├── middleware/
│   │   ├── authentication.ts
│   │   ├── authorization.ts
│   │   ├── error-handler.ts
│   │   ├── request-id.ts
│   │   └── validation.ts
│   ├── routes/
│   │   └── index.ts
│   ├── modules/
│   │   ├── auth/
│   │   ├── users/
│   │   ├── students/
│   │   ├── companies/
│   │   ├── organizations/
│   │   ├── opportunities/
│   │   ├── labs/
│   │   ├── submissions/
│   │   ├── reviews/
│   │   ├── invitations/
│   │   ├── notifications/
│   │   ├── conversations/
│   │   ├── messages/
│   │   ├── files/
│   │   ├── analytics/
│   │   └── ai/
│   ├── database/
│   ├── sockets/
│   ├── errors/
│   └── types/
├── tests/
├── package.json
└── tsconfig.json
```

### Backend module structure

Each module should use this structure where appropriate:

```text
modules/opportunities/
├── opportunity.routes.ts
├── opportunity.controller.ts
├── opportunity.service.ts
├── opportunity.repository.ts
├── opportunity.schema.ts
├── opportunity.types.ts
└── opportunity.test.ts
```

### Backend request flow

```text
HTTP request
    ↓
Request ID middleware
    ↓
Security middleware
    ↓
Authentication middleware
    ↓
Authorization middleware
    ↓
Request validation
    ↓
Controller
    ↓
Service
    ↓
Repository/database
    ↓
Response
```

### Rules

- Controllers must remain thin.
- Business rules belong in services.
- Database queries belong in repositories or database modules.
- Every protected endpoint must check authorization.
- Every request body, query parameter, and path parameter must be validated.
- Errors must use a common error format.
- API responses must follow the documented REST conventions.
- No password, token, or secret may be returned in an API response.
- Backend authorization must never depend only on frontend checks.

## ADR-003: Use a modular monolith

### Decision

The project will initially use a modular monolith with:

```text
apps/web       React + TypeScript frontend
apps/api       Node.js + Express + TypeScript backend
apps/worker    Node.js + TypeScript background worker
```

### Reason

The team is small and the product has many related workflows. A modular monolith is easier to develop, test, deploy, and explain during evaluation than microservices.

### Consequence

The backend must maintain clear module boundaries. Features must communicate through services, domain events, and documented interfaces instead of directly accessing unrelated module internals.

## ADR-004: Use REST for the main API

### Decision

The main frontend/backend communication will use REST APIs under:

```text
/api/v1
```

### Examples

```text
POST /api/v1/auth/register/student
POST /api/v1/auth/register/company
POST /api/v1/auth/login
POST /api/v1/auth/logout

GET  /api/v1/student/profile
PATCH /api/v1/student/profile

GET  /api/v1/opportunities
GET  /api/v1/opportunities/:opportunityId

POST /api/v1/submissions
GET  /api/v1/submissions

POST /api/v1/conversations
GET  /api/v1/conversations/:conversationId/messages
POST /api/v1/conversations/:conversationId/messages
```

## ADR-005: Use Socket.IO for live chat

### Decision

The backend will use Socket.IO running with the Node.js/Express application for live chat delivery.

REST remains responsible for:

- Creating conversations
- Loading conversation history
- Sending messages safely
- Marking conversations as read
- Recovering missed messages

Socket.IO is responsible for:

- Live message delivery
- Unread count events
- Reconnection events
- Conversation room events

Every Socket.IO event must perform authorization checks.