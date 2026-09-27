# GitHub Workflow and CI/CD Guidelines

**Project:** ft_transcendence — Interview Preparation & Company Labs Platform
**Target Audience:** All Development Team Members

This document outlines how our team uses Git, GitHub, and GitHub Actions to collaborate safely, prevent merge conflicts, and ensure we always have a working product for our 42 peer evaluations.

---

## 1. Branching Strategy

We use a Gitflow-inspired branching model to keep our code stable.

*   **`main` branch:** This is the **Production/Evaluation** branch. Code here MUST ALWAYS compile, run via a single `docker-compose up`, and be fully functional. Nobody pushes directly to `main`.
*   **`dev` branch:** This is the **Integration** branch. All completed features are merged here first. This allows us to test how the Frontend, Backend, and shared Infrastructure work together before putting it into `main`.
*   **Feature Branches:** All active development happens here. Branch off of `dev`.
    *   Format: `feature/<feature-name>`
    *   Examples: `feature/student-profile`, `feature/infra-elk`, `feature/oauth-integration`
*   **Bugfix Branches:** For fixing issues found in `dev` or `main`.
    *   Format: `bugfix/<bug-name>`
    *   Example: `bugfix/chat-unread-state`

**How to start a new feature:**
```bash
git checkout dev
git pull origin dev
git checkout -b feature/my-new-feature
```

---

## 2. Conventional Commits

We use structured commit messages. This makes our repository history clean and easy for 42 evaluators to read.

**Format:** `<type>(<scope>): <description>`

**Allowed Types:**
*   `feat`: A new feature (e.g., `feat(ai): add streaming LLM interface`)
*   `fix`: A bug fix (e.g., `fix(auth): resolve 42 OAuth redirect loop`)
*   `chore`: Maintenance, config, or Docker updates (e.g., `chore(docker): update Nginx entrypoint`)
*   `docs`: Documentation changes (e.g., `docs(readme): update API endpoints`)
*   `refactor`: Code changes that neither fix a bug nor add a feature.

*Keep the description under 72 characters and use the imperative mood ("add", not "added").*

---

## 3. Pull Request (PR) Workflow

Direct pushes to `dev` and `main` are blocked by branch protection rules. All code must go through a Pull Request.

1.  **Draft Early:** Open a Draft PR as soon as you push your first commit. This lets the team know what you are working on.
2.  **Keep it Small:** Do not combine multiple unrelated features in one PR. 
3.  **Cross-Role Reviews:** Require at least **one approving review** from a teammate before merging. 
      *   *Example:* If Adam modifies the student profile UI, **Owner to be assigned** should review the data integration, or Jamal should review the access controls.
4.  **Resolve Conflicts Locally:** If your branch is out of date with `dev`, you must pull `dev` into your feature branch and resolve conflicts locally before merging.

---

## 4. GitHub Actions (CI/CD)

The DevOps lead (Mohamed) is configuring GitHub Actions. CI/CD does not replace the `dev` branch; it *protects* it. 

Our GitHub Actions pipeline will automatically run on every Pull Request to `dev` and `main` to enforce the following checks:
*   **Linting/Formatting:** Ensures all code matches our agreed styling.
*   **Build Checks:** Automatically runs `docker compose build` in an isolated environment to guarantee your code hasn't broken the containerized setup.
*   **Testing:** (If applicable) Runs automated unit tests.

**Rule:** You cannot click the "Merge" button on a PR until the GitHub Actions checks show a green checkmark (✅).

---

## 5. Submitting to 42 Intra (Vogsphere)

Because evaluators need to see our entire GitHub commit history and teamwork, we will push our GitHub history directly to the 42 Intra repository at the end of the project.

**Do not start a separate Git repository for Intra.** Use this exact workflow to push our GitHub work to Vogsphere:

```bash
# 1. Add the Intra repository as a secondary remote
git remote add intra <your_vogsphere_url>

# 2. Verify both remotes exist (origin and intra)
git remote -v

# 3. Push the main branch (and the entire commit history) to Intra
git push intra main
```