# A-Plan - Account Plan Management System

A single-page web application for managing account plans with stakeholder tracking, territory assignment, action items, and contact logging. Features admin verification for new users and comprehensive export capabilities.

## Features

✅ **Authentication & Authorization**
- Registration/login restricted to @mylife-diabetescare.com email addresses
- Admin verification required before account activation
- JWT-based session management

✅ **Account Plan Management**
- Create, read, update, delete account plans
- Plan title, creation date, ownership (assignable to users)
- Territory assignment via dropdown

✅ **Stakeholder Management**
- Track stakeholder name, title, influence level, and engagement level
- Link stakeholders to contact logs

✅ **Plan Sections**
- **Current Position:** Text area for context
- **Opportunities:** Dynamic text areas (add/remove multiple)
- **Risks:** Dynamic text areas (add/remove multiple)
- **Actions:** Detailed tracking with action text, date, owner, and status (Not Started, In Progress, Complete, Stuck, Abandoned)
- **Contact Log:** Track interactions with stakeholders by type (In Person, Virtual, Phone, Email, Other), date, and notes

✅ **Export Features**
- Export individual plans to CSV
- Export all plans and territories to CSV
- PDF export (in development)

✅ **Admin Dashboard**
- Authorize/verify new user registrations
- Manage territories (add/delete)
- Import/export plans and territories

## Project Structure

```
A-Plan/
├── index.html              # Main SPA entry point
├── server.js              # Express backend server
├── package.json           # Node.js dependencies
├── .env.example           # Environment variables template
├── README.md              # This file
├── css/
│   └── style.css         # Main stylesheet
├── js/
│   ├── app.js            # Frontend application logic
│   └── admin.js          # Admin dashboard logic
└── db/
    └── schema.sql        # SQLite database schema
```

## Installation

### Prerequisites
- Node.js (v14+)
- npm

### Setup

1. Clone the repository
```bash
git clone https://github.com/sjax90/A-Plan.git
cd A-Plan
```

2. Install dependencies
```bash
npm install
```

3. Create environment file
```bash
cp .env.example .env
```

4. Update `.env` with your settings
```
PORT=3000
JWT_SECRET=your-very-secret-key-here
NODE_ENV=development
```

5. Start the server
```bash
npm start
```

For development with auto-reload:
```bash
npm run dev
```

6. Open browser to `http://localhost:3000`

## Usage

### User Registration & Login
1. Navigate to the registration tab
2. Enter your @mylife-diabetescare.com email address
3. Set a password
4. Wait for admin approval
5. Login with your credentials

### Creating an Account Plan
1. Click "New Plan" button
2. Fill in plan title and select territory
3. Add stakeholders (name, title, influence, engagement)
4. Document current position
5. Add opportunities and risks as needed
6. Create action items with ownership and status tracking
7. Log contacts with stakeholders
8. Click "Save Plan"

### Exporting Data
- **Export Individual Plan:** Open plan and click "Export CSV" or "Export PDF"
- **Export All Plans:** Admin dashboard → Import/Export tab → "Export Plans (CSV)"
- **Export Territories:** Admin dashboard → Import/Export tab → "Export Territories (CSV)"

### Admin Functions
1. Login with admin account
2. Click "Admin" button
3. **Authorize Users:** Review pending registrations and approve/reject
4. **Manage Territories:** Add new territories or delete existing ones
5. **Import/Export:** Bulk import/export plans and territories

## Database Schema

### Users Table
- `id` - Primary key
- `email` - User email (unique, @mylife-diabetescare.com)
- `name` - Full name
- `password` - Hashed password
- `isVerified` - Admin approval status
- `isAdmin` - Admin privileges flag
- `createdAt` - Registration timestamp

### Plans Table
- `id` - Primary key
- `userID` - Foreign key to users
- `title` - Plan title
- `territory` - Territory assignment
- `owner` - Owner user ID
- `currentPosition` - Context text
- `stakeholders` - JSON array
- `opportunities` - JSON array
- `risks` - JSON array
- `actions` - JSON array
- `contactLog` - JSON array
- `dateCreated` - Creation timestamp

### Territories Table
- `id` - Primary key
- `name` - Territory name (unique)
- `createdAt` - Creation timestamp

### Audit Log Table
- `id` - Primary key
- `userID` - Foreign key to users
- `action` - Action description
- `details` - Additional details
- `createdAt` - Timestamp

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user

### Plans
- `GET /api/plans` - Get user's plans
- `GET /api/plans/:id` - Get plan details
- `POST /api/plans` - Create new plan
- `PUT /api/plans/:id` - Update plan
- `DELETE /api/plans/:id` - Delete plan

### Territories
- `GET /api/territories` - Get all territories
- `POST /api/territories` - Create territory (admin only)
- `DELETE /api/territories/:id` - Delete territory (admin only)

### Users
- `GET /api/users` - Get verified users

### Admin
- `GET /api/admin/users` - Get all users (admin only)
- `POST /api/admin/users/:id/approve` - Approve user (admin only)
- `POST /api/admin/users/:id/reject` - Reject user (admin only)
- `GET /api/admin/export/plans` - Export all plans (admin only)
- `POST /api/admin/import/plans` - Import plans (admin only)
- `GET /api/admin/export/territories` - Export territories (admin only)
- `POST /api/admin/import/territories` - Import territories (admin only)

## Security Considerations

- All passwords are hashed using bcryptjs
- JWT tokens expire after 24 hours
- Email domain is restricted to @mylife-diabetescare.com
- Admin verification required for account activation
- Protected endpoints require valid JWT token
- Admin-only endpoints require admin flag

## Future Enhancements

- [ ] PDF export functionality
- [ ] Real-time collaboration
- [ ] Email notifications for action items
- [ ] Plan templates
- [ ] Advanced reporting and analytics
- [ ] Two-factor authentication
- [ ] Plan sharing and permissions
- [ ] Activity timeline/history

## Development

Run in development mode with auto-reload:
```bash
npm run dev
```

## License

MIT

## Support

For issues, questions, or suggestions, please open an issue on GitHub.