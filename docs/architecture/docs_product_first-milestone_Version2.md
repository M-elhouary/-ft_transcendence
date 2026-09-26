# First milestone

## Goal

A student and a company can create accounts, complete profiles, and access their correct dashboards.

## Cards

### Architecture

| Card | Owner | Reviewer |
|---|---|---|
| Confirm monorepo structure | Jamal | All |
| Confirm API conventions | Jamal | Hicham |
| Confirm database entities | Hicham | Jamal |
| Confirm local Docker environment | Mouhamed | Jamal |
| Create frontend application skeleton | Adam | Salah |
| Create backend application skeleton | Hicham | Jamal |

### Infrastructure

| Card | Owner | Acceptance criteria |
|---|---|---|
| Docker Compose PostgreSQL | Mouhamed | Database starts locally |
| Docker Compose Redis | Mouhamed | Redis accepts connections |
| Environment variable template | Mouhamed | No secrets committed |
| API health endpoint | Hicham | `/health` returns service status |
| Frontend development setup | Adam | React app starts locally |

### Authentication

| Card | Owner | Acceptance criteria |
|---|---|---|
| User model and migration | Hicham | Migration runs successfully |
| Password hashing | Jamal | Password is never stored in plain text |
| Student registration | Jamal + Adam | Student can register |
| Company registration | Jamal + Salah | Company can register |
| Sign-in and sign-out | Jamal | Session is created and destroyed securely |
| Role protection middleware | Jamal | Incorrect roles receive 403 |
| Password recovery design | Jamal | Flow and token rules documented |

### Profiles

| Card | Owner | Acceptance criteria |
|---|---|---|
| Student profile model | Hicham | Required and optional fields exist |
| Student profile UI | Adam | Student can edit profile |
| Company profile model | Hicham | Company information is persisted |
| Company profile UI | Salah | Company can edit profile |
| Profile completion calculation | Hicham | Required fields are checked consistently |
| Profile access tests | Jamal | Unrelated users cannot access private profiles |

## Milestone demonstration

At the end of the milestone:

1. Student registers.
2. Student signs in.
3. Student edits their profile.
4. Student sees incomplete required fields.
5. Company registers.
6. Company signs in.
7. Company edits its profile.
8. Admin can see pending company verification.
9. Student cannot access company administration.
10. Company cannot access another company's profile.