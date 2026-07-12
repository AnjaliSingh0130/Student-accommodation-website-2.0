# 🏠 StayEase — Student Accommodation Website

A responsive web application that helps students find, filter, and shortlist verified PG/hostel accommodation near their college. Built as a minor project for BCA Semester IV, following the Internshala "Student Accommodation Website" brief.

**Author:** Anjali Singh

---

## 📌 Problem Statement

Students moving to a new city for college often struggle to find safe, verified, and reasonably-priced accommodation, and typically end up relying on brokers or word-of-mouth with little clarity on price or amenities. StayEase gives students a single platform to search, compare, and shortlist PG/hostel listings by city, budget, and gender preference — with instant filtering and a one-click "Interested" (shortlist) button, no page reloads required.

## ✨ Features

- **User Registration & Login** — secure signup/login with hashed passwords (PHP `password_hash`)
- **Search & Filters** — filter listings by city, maximum budget, and gender, applied instantly via AJAX
- **Property Detail Page** — dedicated page per listing with photos, description, amenities, and rating
- **Shortlist / "Interested" Button** — a React component that marks/unmarks a property as interested, without reloading the page
- **Responsive UI** — built with Bootstrap 5, works on mobile, tablet, and desktop
- **Offline Demo Mode** — if no PHP/MySQL server is running, the site automatically falls back to bundled sample data (`frontend/js/data.json`), so it can still be viewed by just opening the HTML file

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5, CSS3, Bootstrap 5, JavaScript (Fetch API / AJAX) |
| Component | React (compiled with esbuild into a standalone bundle — no CDN dependency) |
| Backend | PHP (PDO) |
| Database | MySQL |

## 📸 Screenshots

| Property Listing | Property Detail |
|---|---|
| ![Listing](screenshots/01_property_listing.png) | ![Detail](screenshots/02_property_detail.png) |

| AJAX — Marked as Interested | AJAX — Filter Applied |
|---|---|
| ![Interested](screenshots/03_ajax_interested_marked.png) | ![Filter](screenshots/04_ajax_filter_applied.png) |

## 🗂️ Folder Structure

```
StudentAccommodationWebsite/
├── sql/
│   └── schema.sql                 # Database schema + sample data (5 tables, 5 properties)
├── backend-php/
│   ├── config/db.php              # MySQL connection (PDO)
│   └── api/
│       ├── properties.php         # GET  — list + filter properties
│       ├── property_detail.php    # GET  — single property + amenities
│       ├── signup.php             # POST — register a user
│       ├── login.php              # POST — authenticate a user
│       └── interest.php           # POST — toggle shortlist (AJAX)
├── frontend/
│   ├── index.html                 # Property Listing page
│   ├── property-detail.html       # Property Detail page
│   ├── login.html                 # Login page
│   ├── register.html              # Register page
│   ├── css/style.css
│   ├── js/main.js                 # AJAX calls + DOM rendering
│   ├── js/data.json                # Offline/demo sample data
│   └── react/
│       ├── src/ShortlistApp.jsx    # React "Interested" button (source)
│       └── dist/bundle.js          # Compiled, dependency-free bundle
├── screenshots/                   # Listing, detail, and AJAX interaction screenshots
├── Brief_Project_Document.docx    # Full project write-up
├── LICENSE
└── README.md
```

## 🗄️ Database Design

Five normalized tables:

- `users(id, name, email, password, phone)` — registered students
- `properties(id, name, city, price, gender, rating, description, image)` — PG/hostel listings
- `amenities(id, name)` — master list (WiFi, AC, Laundry, etc.)
- `property_amenities(property_id, amenity_id)` — many-to-many link
- `interested_users(user_id, property_id)` — the shortlist relationship

Full schema with foreign keys and sample data is in [`sql/schema.sql`](sql/schema.sql).

## 🚀 Running It Locally

1. Install a local PHP + MySQL stack (XAMPP / WAMP / MAMP), or run `php -S localhost:8000` from the project root.
2. Import [`sql/schema.sql`](sql/schema.sql) into MySQL — this creates the `student_accommodation` database with sample data already loaded.
3. Open `backend-php/config/db.php` and update `$DB_USER` / `$DB_PASS` to match your MySQL credentials.
4. Serve the project through your PHP server and open `frontend/index.html` in the browser.
   - Alternatively, just double-click `frontend/index.html` to open it directly — the site will automatically fall back to the bundled sample data in demo mode (no MySQL needed), which is handy for a quick look.

## 🔌 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/backend-php/api/properties.php` | List properties, with optional `city`, `budget`, `gender` query params |
| GET | `/backend-php/api/property_detail.php?id=<id>` | Full detail for one property, including amenities |
| POST | `/backend-php/api/signup.php` | Register a new user |
| POST | `/backend-php/api/login.php` | Authenticate a user |
| POST | `/backend-php/api/interest.php` | Toggle a property's "Interested" (shortlist) status |

## 🔮 Future Scope

- Map integration to show each property's exact location and distance from college
- Online booking system with confirmation workflow
- Payment gateway integration for booking deposits / rent

## 📄 Submitting on Internshala

Internshala's brief asks for 5 deliverables:

| Deliverable | Status |
|---|---|
| Database schema file (`.sql`) | ✅ `sql/schema.sql` |
| Screenshots (listing, detail, AJAX) | ✅ `screenshots/` |
| Brief project document | ✅ `Brief_Project_Document.docx` |
| GitHub repository link | ⬜ Push this project to a new GitHub repo (see below) |
| Live project URL | ⬜ Deploy on a free PHP + MySQL host (see below) |

**1. Push to GitHub:**
```bash
git init
git add .
git commit -m "Initial commit: StayEase - Student Accommodation Website"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

**2. Deploy live (free PHP + MySQL hosts):** InfinityFree, 000webhost, or Hostinger's free tier all work.
- Upload `backend-php/` and `frontend/` via their File Manager or FTP.
- Use their phpMyAdmin to import `sql/schema.sql`.
- Update `backend-php/config/db.php` with the credentials they provide.
- Your live URL will look like `https://yourname.infinityfreeapp.com/frontend/index.html`.

Once both are ready, add the links to Section 10 of `Brief_Project_Document.docx` before submitting.

## 👩‍💻 Author

**Anjali Singh** — BCA Student

## 📃 License

This project is licensed under the [MIT License](LICENSE).
