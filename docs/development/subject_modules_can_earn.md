📊 **Our project features and the subject modules they can earn**

Team, this maps each module to the features we must implement to claim its points.

📖 Reference: **ft_transcendence v21.2**. Pages below use the subject’s **printed numbering**.

**1. Frontend + backend frameworks — 2 points**
📍 §IV.1 — page 12

We build our student/company interfaces using a frontend framework and our API using a backend framework. The team still needs to confirm the stack.

Both sides together count as **2 points**, not additional points per framework or service.

**2. ORM — 1 point**
📍 §IV.1 — page 12

Use an ORM to implement database access for students, companies, opportunities, labs, submissions, reviews and messages, with clearly defined relationships.

**3. Advanced search — 1 point**
📍 §IV.1 — page 13

Students can discover opportunities and labs using:
• Filters such as skills, location and career path.
• Sorting, such as newest or approaching deadline.
• Pagination.

Exact filters remain to be agreed. A search box alone is insufficient.

**4. File upload and management — 1 point**
📍 §IV.1 — page 13

Support files such as student CVs, profile pictures, company logos and requested submission attachments.

We need:
• Multiple supported file types.
• Frontend and backend validation of type, size and format.
• Secure storage and permission checks.
• Previews where appropriate.
• Upload progress indicators.
• File deletion.

Example: a recruiter can access an authorized candidate’s CV, but cannot access unrelated private documents.

**5. Advanced permissions — 2 points**
📍 §IV.3 — page 14

Implement user administration and role management:
• Admins can view, edit and delete users through authorized actions.
• Students manage their own profiles and submissions.
• Recruiters access their company’s permitted features.
• Company owners manage recruiter access.
• Different roles see and perform different actions.

Permissions must be enforced in the backend, not only by hiding buttons.

**6. Organization system — 2 points**
📍 §IV.3 — page 14

Treat each company as an organization:
• Create, view, edit and delete organizations.
• Add and remove recruiters.
• Allow authorized members to create, read and update company resources.
• Keep opportunities, labs and candidate reviews scoped to the correct company.

A company profile without membership management is insufficient.

**7. OAuth 2.0 — 1 point**
📍 §IV.3 — page 14

Students can sign in using a selected provider such as GitHub or 42.

Implement the authorization and callback flow, connect the identity to the correct account, and handle cancellation or failure. Two providers do not mean two points.

**8. Complete LLM interface — 2 points**
📍 §IV.4 — page 15

Our AI features:
• Company requirements → editable lab draft with tasks, deliverables and review criteria.
• Interview practice → questions and feedback on student answers.

To claim the module, we must implement:
• Generation based on user input.
• Proper streamed responses.
• Error handling.
• Server-side rate limiting.

The company approves generated labs before publication. All these generation features share **one 2-point module**.

**9. Real-time features — 2 points**
📍 §IV.1 — page 12

Company-initiated chat:
• An authorized company starts a conversation with an eligible student.
• The student can reply.
• Messages appear for connected participants without refreshing.
• Connections and disconnections are handled gracefully.
• Messages are broadcast efficiently to authorized participants.

We still need to finalize contact eligibility. A message database with manual refreshing is insufficient.

**10. Advanced analytics — 2 points**
📍 §IV.8 — page 19

Companies monitor their recruitment activity:
• Submissions per lab.
• Completed and pending reviews.
• Invitations sent.
• Changes over time.

The dashboard needs interactive charts, real-time updates, exports and customizable date ranges/filters. Static counters alone are insufficient. It does not rank candidates.

**11. ELK log management — 2 points**
📍 §IV.7 — pages 18–19

Centralize platform logs:
• Logstash collects and transforms logs.
• Elasticsearch stores and indexes them.
• Kibana provides views and dashboards.
• Configure retention and archiving.
• Secure access to all components.

Example: investigate a failed submission or AI request without exposing passwords, tokens or private message content.

**12. Prometheus + Grafana — 2 points**
📍 §IV.7 — page 19

Monitor the application and infrastructure:
• Prometheus collects metrics through exporters/integrations.
• Grafana shows custom dashboards.
• Alerts identify failures or abnormal behavior.
• Grafana access is secured.

Useful metrics include request errors, response times, service availability and AI generation failures. Installing the tools alone is insufficient.

**13. Health, status, backups and recovery — 1 point**
📍 §IV.7 — page 19

Implement:
• Service health checks.
• A status page.
• Automated backups.
• Documented disaster recovery procedures.

We should demonstrate restoring backed-up data. A health endpoint alone does not cover the module.

**14. Optional RAG system — +2 points**
📍 §IV.4 — page 15

Build a preparation assistant where students ask technical questions and receive answers grounded in retrieved documents.

We need:
• A substantial, relevant knowledge collection.
• Document ingestion and indexing.
• Retrieval of relevant passages.
• Answer generation using those passages.
• A working user Q&A interface.

We also plan source references and private-document access controls. One README prototype is a starting point, not our complete module.

**Decision: implement the LLM interface first; add RAG only if time remains.**

🧮 **Calculation**

• Web: **7 points**
• User Management: **5 points**
• LLM interface: **2 points**
• DevOps: **5 points**
• Analytics: **2 points**

✅ **Total without RAG: 21 potential points**
✅ **Total with RAG: 23 potential points**

The subject requires **14 points** (§IV, p.10), with at most **5 additional bonus points** (§VII, p.30).

⚠️ **These are planned points, not awarded points.** Incomplete modules count as zero.

Basic registration, Docker deployment and ordinary CI/CD do not add separate points here. We are not claiming the standard user-management or user-interaction modules because their required friends features are outside our current plan. The editor, terminal and sandboxes are also excluded from this calculation.

Each module needs an owner, acceptance criteria, a working demonstration and an explanation in the README.