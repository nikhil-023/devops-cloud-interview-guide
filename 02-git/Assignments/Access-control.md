# A Clean Example of a Production-Ready Access Control Design

ORG LEVEL
 ├── Teams
 │    ├── DevOps → Admin
 │    ├── Leads → Maintainer
 │    ├── Developers → Contributor
 │    ├── QA → Reader
 │    └── Security → Approver
 └── Policies
      ├── Enforce SSO + MFA
      ├── No direct pushes to main
      ├── Signed commits required
      └── Protected secrets

BRANCH LEVEL
 ├── main → Protected
 │       ├── No direct push
 │       ├── PR only
 │       ├── 2 reviewers required
 │       ├── CI must pass
 │       └── Code scan mandatory
 └── feature/* → Open to devs
         └── No protection

ENV LEVEL
 ├── Dev → open access, auto deploy
 ├── Stage → lead approval
 └── Prod → restricted to DevOps + leads