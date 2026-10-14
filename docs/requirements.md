# AppointFlow Dashboard - Requirements

## 1. Purpose

The business-side application where businesses manage their profile, services, staff, working hours, and appointments. The data entered here is what customers see and book on the AppointFlow Website.

This document covers the **dashboard only**. The website has its own requirements file.

## 2. Users and Roles

| Role | Description |
| --- | --- |
| Super Admin | Platform owner. Reviews, approves, and blocks businesses. Uses Django Admin in the MVP. |
| Business Administrator | Owner or manager of one business. Full control of that business's data. |
| Business Staff | Employee of one business. Sees only their own schedule and appointments. |

Customers do not use the dashboard. They use the website.

## 3. Business Onboarding

1. A business submits a registration request from the dashboard.
2. The request is saved with status `pending`.
3. The Super Admin reviews it and approves or rejects it.
4. On approval, the business administrator can log in.
5. The administrator sets up services, staff, and working hours.
6. Only approved businesses appear on the public website.

For the first few clients, the Super Admin may create accounts manually instead.

## 4. Access Control (RBAC)

| Feature | Super Admin | Business Admin | Staff |
| --- | --- | --- | --- |
| Approve / block businesses | Yes | No | No |
| Business profile | No | Yes | No |
| Services | No | Yes | No |
| Staff management | No | Yes | No |
| Working hours, breaks, days off | No | Yes | No |
| All appointments of the business | No | Yes | No |
| My schedule | No | No | Yes |
| Update appointment status | No | Yes | Own appointments only |
| Overview | Platform-wide (later) | Own business | Own day |

Rules:

1. The UI shows menu items based on the user's role.
2. The backend enforces the role on every API request. A staff member opening an admin URL must get `403 Forbidden`.
3. A user can only access data of their own business.

## 5. Pages

### Public

1. Register (business request)
2. Login

### Business Administrator

3. Overview: upcoming appointments, daily booking totals
4. Business profile
5. Services: list, add, edit, delete (name, duration, price)
6. Staff: list, add, edit, deactivate; create staff logins
7. Working hours: per staff member, with breaks and days off
8. Appointments: list with filters (date, staff, status); view, cancel, reschedule, update status

### Business Staff

9. Overview: today's appointments
10. My schedule: day and week calendar
11. Appointment detail: mark as completed or cancelled

## 6. Functional Requirements

1. Business admins can create and edit the business profile.
2. Business admins can add services with name, duration, and price.
3. Business admins can create staff accounts and assign services to staff.
4. Business admins can set working hours, breaks, and days off for each staff member.
5. Business admins can see all appointments of their business and filter them.
6. Staff can see only their own appointments.
7. Appointment statuses: `pending`, `confirmed`, `completed`, `cancelled`.
8. Business admins and staff can mark appointments as completed or cancelled.
9. The overview shows upcoming appointments and the total bookings per day.

## 7. Business Rules

1. A staff member cannot have overlapping bookings.
2. Appointment times must respect working hours.
3. Each business can access only its own private data.
4. Cancelled appointments release their time slots.
5. Changing working hours must not silently break existing future appointments. The admin is warned about conflicts.

## 8. Non-Functional Requirements

- **Security:** authentication on all dashboard pages, role-based access control, data isolation between businesses
- **Responsive:** usable on tablet and mobile (staff may check schedules on a phone)
- **Usability:** clear tables, filters, and confirmation before destructive actions
- **Maintainability:** typed code (TypeScript), reusable components for tables, forms, and calendar

## 9. Out of Scope for the MVP

- Reports and analytics
- Payments
- Email or WhatsApp reminders
- Super Admin screens inside the dashboard (Django Admin is used instead)

## 10. Technologies

| Part | Technology |
| --- | --- |
| Framework | Next.js (React) + TypeScript |
| Styling | Tailwind CSS |
| API | REST (Django REST Framework) |
| Version control | Git + GitHub |

## 11. Related Projects

- `appointflow-website`: customer side
- `appointflow-backend`: Django REST API and PostgreSQL database
