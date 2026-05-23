# श्रम सेवा (Shram Sewa) — Complete Setup Guide


## What's been completed
- ✅ User auth (register, login, JWT, role-based routing)
- ✅ Job postings with map pin (Leaflet/OpenStreetMap, no API key)
- ✅ Geolocation — "Jobs Near Me" using browser GPS + MongoDB 2dsphere index
- ✅ Apply for jobs with bid amount and message
- ✅ Approve / reject applicants (with notifications)
- ✅ Mark job as Completed
- ✅ Rating & Review system (5-star, post-completion only)
- ✅ In-app Notifications (bell icon, unread badge, 30s polling)
- ✅ Admin dashboard (verify users, manage all users)
- ✅ Freelancer dashboard with real earnings data and reviews
- ✅ Earnings page wired to real application data with chart

---


## Prerequisites
- Node.js 18+
- MongoDB Atlas account (free tier works)
- Git

---


## Backend Setup

```bash
cd backend
npm install
```

Create `backend/.env`:
```
MONGO_URI=mongodb+srv://<user>:<password>@cluster0.xxxxx.mongodb.net/shramsewa?retryWrites=true&w=majority
JWT_SECRET=your_super_secret_key_here
ADMIN_EMAIL=admin@shramsewa.com
ADMIN_PASSWORD=admin123
PORT=5000
```

**Important — create the 2dsphere index** (run once in MongoDB Atlas shell or Compass):
```javascript
db.jobs.createIndex({ coordinates: "2dsphere" })
```

Start backend:
```bash
npm run dev
```

---


## Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

---


## Test Credentials
- Admin: use ADMIN_EMAIL and ADMIN_PASSWORD from .env
- Register a Client account → get verified by admin → post jobs
- Register a Freelancer account → get verified by admin → apply for jobs

---


## Key New Features Explained

### Geolocation (Near Me)
- Hirers can pin job location on a Leaflet map when posting
- Freelancers click "Jobs Near Me" → browser asks for GPS → shows jobs within 10km
- Requires the 2dsphere MongoDB index (see above)



### Ratings & Reviews
- Only works AFTER a job is marked Completed (green tick button in Manage Jobs)
- Hirer clicks ⭐ Review button on an approved applicant
- Rating auto-updates the freelancer's profile average

### Notifications
- Bell icon in top header with live unread count
- Auto-refreshes every 30 seconds
- Triggered by: applications, approvals, rejections, completions, reviews

