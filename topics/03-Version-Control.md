# Version Control & Collaboration

This module focuses on Git and modern collaboration practices using GitHub/GitLab.  
Strong version control skills are essential for every DevOps engineer — you will use Git daily for infrastructure code, pipelines, application code, and documentation.

### Why Version Control Matters in DevOps
- Enables collaboration without conflicts
- Provides full history and rollback capability
- Supports CI/CD pipelines (every commit can trigger builds/tests)
- Forms the foundation for GitOps (later modules)
- Helps maintain audit trails and code quality

### Core Topics

#### 1. Git Fundamentals (Quick Revision)
- `git init`, `git clone`, `git status`, `git add`, `git commit`
- `git push`, `git pull`, `git fetch`
- `.gitignore` best practices

#### 2. Advanced Git Workflows
- **Branching Strategies**
  - Feature branches
  - GitFlow (main + develop + feature/release/hotfix)
  - Trunk-Based Development (short-lived branches)
  - GitHub Flow (simple and popular for DevOps teams)

- **Merging Techniques**
  - Merge commits
  - Rebase (`git rebase`)
  - Squash commits
  - Cherry-pick

- **Undoing Changes**
  - `git reset` (soft, mixed, hard)
  - `git revert`
  - `git reflog` (recovery tool)

#### 3. Collaboration Features (GitHub / GitLab)
- Pull Requests (PRs) / Merge Requests (MRs)
- Code reviews and approvals
- Protected branches (prevent direct pushes to main)
- Branch policies and required status checks
- Issues and project boards
- GitHub Projects / Milestones

#### 4. Advanced Git Features Useful for DevOps
- Git Hooks (pre-commit, pre-push)
- Git Submodules (when needed)
- Monorepo vs Multi-repo strategies
- Large File Storage (Git LFS) for binaries
- Signing commits (GPG)

#### 5. Common DevOps Git Practices
- Keep commits small and focused (Atomic commits)
- Write meaningful commit messages
- Use conventional commits (`feat:`, `fix:`, `chore:`, `docs:`)
- Keep main branch always deployable
- Feature flags for long-running features

### Hands-on Practice Recommendations
1. Create a new repository and practice different branching strategies.
2. Simulate a team workflow:
   - Create a feature branch
   - Make changes and commit
   - Open a Pull Request
   - Review and merge using squash/rebase
3. Break something intentionally and recover using `git reflog` or `git reset`.
4. Set up branch protection rules on your repository.

### Next Steps After This Module
- Move to **Module 03: CI & Build Automation** (GitHub Actions focus)
- Start using Git properly in all future challenges and projects

### Self-Assessment Questions
- What is the difference between `git merge` and `git rebase`?
- When would you use `git reset --hard` vs `git revert`?
- How do you protect the main branch from direct pushes?
- What makes a good commit message in a DevOps team?

### Recommended Resources
- Official Git Documentation: https://git-scm.com/doc
- Pro Git Book (free): https://git-scm.com/book/en/v2
- GitHub Skills / Learning Lab (free interactive tutorials)
- Conventional Commits: https://www.conventionalcommits.org

---

**Module Progress**
- [x] Module 01 – Foundations & Culture + Linux Mastery
- [ ] Module 02 – Version Control & Collaboration ← **You are here**

When you finish this module, move to **topics/03-ci-cd.md**.

Questions or suggestions? Open an issue in the repository.

**Next Action for You (the teacher)**:  
Would you like me to create:
- A **Git Challenge** to go with this module?
- Or directly start **topics/03-ci-cd.md** (CI/CD with GitHub Actions)?

Just reply with your choice.
