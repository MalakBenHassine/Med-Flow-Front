
This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).


## 🚀 Getting Started


npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev


Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 🔐 Authentication Workflow

This project integrates **NextAuth** with a **Django REST API** for authentication, session management, and role-based access control.

### 🧩 1. Login Process


User → Login Page (/login) → signIn() → authorize() → Django API


- The user fills out the login form.  
- The `signIn()` method (provided by **NextAuth**) sends credentials to the backend.  
- The `authorize()` function in `NextAuthConfig.tsx` sends a POST request to:

  /api/accounts/login/

- If Django validates the credentials, it returns user data and a JWT token.

---

### 🧠 2. Session & JWT Callbacks


NextAuth → jwt callback → session callback → Available in useSession()


- The `jwt` callback stores extra user data (like `role`, `id`, `accessToken`) inside the token.  
- The `session` callback exposes these values in the client session.  
- You can access session data anywhere with:

  import { useSession } from "next-auth/react";
  const { data: session } = useSession();
  console.log(session?.user);


---

### 🛡️ 3. Route Protection

Protected routes (e.g. `/admin/dashboard`) are handled through `middleware.ts`.

- If the user is **not authenticated**, they are redirected to `/login`.  
- Role-based logic ensures users only access authorized pages.  
  Example:

  Admin → /admin/dashboard
  Doctor → /doctor/dashboard
  Patient → /patient/profile


---

## 📁 Key Files Overview

src/app/api/auth/NextAuthConfig.tsx   # Handles login logic and token creation
src/middleware.ts                     # Protects routes and manages role-based redirection
src/app/login/page.tsx                # Login page UI and signIn() handler
src/app/admin/dashboard/page.tsx      # Example of a protected route for admins


---

## ⚙️ Environment Variables

Create a `.env.local` file:


BACKEND_URL=http://127.0.0.1:8000
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your_generated_secret
```

Generate a secure secret with:


npx auth secret
```

---

## 🧾 Summary


✅ Secure login using Django backend
✅ JWT-based session management via NextAuth
✅ Role-based route protection with middleware
✅ No localStorage – uses encrypted cookies
✅ Easy session access with useSession()


---

## 📚 Learn More


Next.js Docs:        https://nextjs.org/docs
NextAuth.js Docs:    https://next-auth.js.org
Django REST Framework: https://www.django-rest-framework.org

# med-flow-front



## Getting started

To make it easy for you to get started with GitLab, here's a list of recommended next steps.

Already a pro? Just edit this README.md and make it your own. Want to make it easy? [Use the template at the bottom](#editing-this-readme)!

## Add your files

* [Create](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#create-a-file) or [upload](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#upload-a-file) files
* [Add files using the command line](https://docs.gitlab.com/topics/git/add_files/#add-files-to-a-git-repository) or push an existing Git repository with the following command:

cd existing_repo
git remote add origin https://gitlab.com/MalakBenHassine/med-flow-front.git
git branch -M main
git push -uf origin main
```

## Integrate with your tools

* [Set up project integrations](https://gitlab.com/MalakBenHassine/med-flow-front/-/settings/integrations)

## Collaborate with your team

* [Invite team members and collaborators](https://docs.gitlab.com/ee/user/project/members/)
* [Create a new merge request](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html)
* [Automatically close issues from merge requests](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically)
* [Enable merge request approvals](https://docs.gitlab.com/ee/user/project/merge_requests/approvals/)
* [Set auto-merge](https://docs.gitlab.com/user/project/merge_requests/auto_merge/)

## Test and Deploy

Use the built-in continuous integration in GitLab.

* [Get started with GitLab CI/CD](https://docs.gitlab.com/ee/ci/quick_start/)
* [Analyze your code for known vulnerabilities with Static Application Security Testing (SAST)](https://docs.gitlab.com/ee/user/application_security/sast/)
* [Deploy to Kubernetes, Amazon EC2, or Amazon ECS using Auto Deploy](https://docs.gitlab.com/ee/topics/autodevops/requirements.html)
* [Use pull-based deployments for improved Kubernetes management](https://docs.gitlab.com/ee/user/clusters/agent/)
* [Set up protected environments](https://docs.gitlab.com/ee/ci/environments/protected_environments.html)

***

# Editing this README

When you're ready to make this README your own, just edit this file and use the handy template below (or feel free to structure it however you want - this is just a starting point!). Thanks to [makeareadme.com](https://www.makeareadme.com/) for this template.

## Suggestions for a good README

Every project is different, so consider which of these sections apply to yours. The sections used in the template are suggestions for most open source projects. Also keep in mind that while a README can be too long and detailed, too long is better than too short. If you think your README is too long, consider utilizing another form of documentation rather than cutting out information.

## Name
Choose a self-explaining name for your project.

## Description
Let people know what your project can do specifically. Provide context and add a link to any reference visitors might be unfamiliar with. A list of Features or a Background subsection can also be added here. If there are alternatives to your project, this is a good place to list differentiating factors.

## Badges
On some READMEs, you may see small images that convey metadata, such as whether or not all the tests are passing for the project. You can use Shields to add some to your README. Many services also have instructions for adding a badge.

## Visuals
Depending on what you are making, it can be a good idea to include screenshots or even a video (you'll frequently see GIFs rather than actual videos). Tools like ttygif can help, but check out Asciinema for a more sophisticated method.

## Installation
Within a particular ecosystem, there may be a common way of installing things, such as using Yarn, NuGet, or Homebrew. However, consider the possibility that whoever is reading your README is a novice and would like more guidance. Listing specific steps helps remove ambiguity and gets people to using your project as quickly as possible. If it only runs in a specific context like a particular programming language version or operating system or has dependencies that have to be installed manually, also add a Requirements subsection.

## Usage
Use examples liberally, and show the expected output if you can. It's helpful to have inline the smallest example of usage that you can demonstrate, while providing links to more sophisticated examples if they are too long to reasonably include in the README.

## Support
Tell people where they can go to for help. It can be any combination of an issue tracker, a chat room, an email address, etc.

## Roadmap
If you have ideas for releases in the future, it is a good idea to list them in the README.

## Contributing
State if you are open to contributions and what your requirements are for accepting them.

For people who want to make changes to your project, it's helpful to have some documentation on how to get started. Perhaps there is a script that they should run or some environment variables that they need to set. Make these steps explicit. These instructions could also be useful to your future self.

You can also document commands to lint the code or run tests. These steps help to ensure high code quality and reduce the likelihood that the changes inadvertently break something. Having instructions for running tests is especially helpful if it requires external setup, such as starting a Selenium server for testing in a browser.

## Authors and acknowledgment
Show your appreciation to those who have contributed to the project.

## License
For open source projects, say how it is licensed.

## Project status
If you have run out of energy or time for your project, put a note at the top of the README saying that development has slowed down or stopped completely. Someone may choose to fork your project or volunteer to step in as a maintainer or owner, allowing your project to keep going. You can also make an explicit request for maintainers.
