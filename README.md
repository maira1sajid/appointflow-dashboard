# AppointFlow Dashboard

The business-side dashboard of **AppointFlow**, a multi-business appointment platform. Businesses use it to manage their profile, services, staff, working hours, and appointments. One app serves multiple roles, and each role sees only what it is allowed to see (RBAC).

> Looking for the customer side? See the **AppointFlow Website** repository (`appointflow-website`). Full requirements for this project: [docs/requirements.md](docs/requirements.md).

## How the platform is organized

| Project | Who uses it | Purpose |
| --- | --- | --- |
| `appointflow-website` | Customers | Browse businesses, book, cancel, and reschedule appointments |
| **`appointflow-dashboard` (this repo)** | Business Admin, Staff (and Super Admin later) | Manage business data and appointments |
| `appointflow-backend` | Both frontends | Django REST API and PostgreSQL |

## Roles (RBAC)

| Role | What they can do |
| --- | --- |
| Super Admin (platform owner) | Review and approve or block businesses. In the MVP this is done in Django Admin. |
| Business Administrator | Manage the business profile, services, staff, working hours, all appointments, and reports. |
| Business Staff | View their own schedule and mark their appointments as completed or cancelled. |

The backend also checks the role on every API request. Hiding menu items in the UI is not security.

## Features (MVP)

- Business registration request and login
- Overview with upcoming appointments and daily booking totals
- Business profile management
- Service management (name, duration, and price)
- Staff management (create staff accounts)
- Working hours, breaks, and days off
- Appointments list with filters and status updates (completed or cancelled)
- Staff schedule (day and week calendar)

## Tech Stack

| Part | Technology |
| --- | --- |
| Framework | Next.js (React) and TypeScript |
| Styling | Tailwind CSS |
| API | REST (Django REST Framework backend) |
| Version control | Git and GitHub |

## Getting Started

### Prerequisites

- Node.js 20 or newer
- npm
- The AppointFlow backend running locally

### Installation

```bash
git clone https://github.com/<your-username>/appointflow-dashboard.git
cd appointflow-dashboard
npm install
```

### Environment variables

Create a `.env.local` file in the project root:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000/api
NEXT_PUBLIC_WEBSITE_URL=http://localhost:3000
```

`.env*` files are ignored by git. Never commit them.

### Run the development server

The website uses port 3000, so run the dashboard on port 3001:

```bash
npm run dev -- -p 3001
```

Open [http://localhost:3001](http://localhost:3001).

Also add the dashboard origin (`http://localhost:3001`) to the backend's CORS settings.

### Other scripts

```bash
npm run build   # production build
npm run start   # run the production build
npm run lint    # run ESLint
```

## Project Structure

```text
appointflow-dashboard/
├── app/          # Next.js App Router pages and layouts
├── public/       # Static assets
├── docs/         # Project documentation
└── ...           # Config files
```

## Roadmap

1. Finalize requirements
2. Build login and role-based layout (menus per role)
3. Build services, staff, and working hours pages
4. Build appointments list and staff schedule
5. Build overview with daily totals
6. Test and deploy

Later phases: reports, analytics, notifications, and a Super Admin section inside the dashboard.

## License

Proprietary. All rights reserved.
