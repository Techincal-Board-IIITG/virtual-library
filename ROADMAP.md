# Virtual Library

A centralized academic resource platform for the college.

The idea is simple: keep notes, assignments, PYQs, lab files, question papers, and other academic resources in one place instead of having them scattered across WhatsApp groups, Google Drive links, Telegram, and random folders.

---

## Roadmap

### 1. Project Setup

- [ ] Create GitHub repository
- [ ] Set up frontend
- [ ] Set up Spring Boot backend
- [ ] Set up PostgreSQL
- [ ] Set up `.env` / environment configuration
- [ ] Set up Git branches
- [ ] Add basic README
- [ ] Add `.gitignore`
- [ ] Set up Docker for local development

---

### 2. Database

Start with the basic academic structure.

- [ ] User
- [ ] Department
- [ ] Semester
- [ ] Subject
- [ ] Resource
- [ ] Resource category

Basic relationship:

```text
Department
    |
    +-- Semester
          |
          +-- Subject
                |
                +-- Resource
```

Resource categories:

```text
Notes
Assignments
PYQs
Lab
Question Papers
Books
Slides
Other
```

- [ ] Create entities
- [ ] Create repositories
- [ ] Create migrations with Flyway
- [ ] Add relationships
- [ ] Add database indexes where needed

---

### 3. Authentication

- [ ] Register
- [ ] Login
- [ ] Password hashing
- [ ] JWT authentication
- [ ] Refresh token
- [ ] Logout
- [ ] Current-user endpoint
- [ ] Role-based access

Roles:

```text
USER
ADMIN
```

Later:

```text
MODERATOR
```

---

### 4. Academic Structure

Admin should be able to create and manage:

```text
Department
    ↓
Semester
    ↓
Subject
```

- [ ] Department CRUD
- [ ] Semester CRUD
- [ ] Subject CRUD
- [ ] Assign subjects to semesters
- [ ] Enable / disable subjects
- [ ] Seed initial college data

---

### 5. Resource System

This is the main part of the application.

A resource should contain things like:

```text
Title
Description
Subject
Category
Semester
Uploader
File
Tags
Created At
Updated At
```

- [ ] Create resource
- [ ] Get resource
- [ ] Update resource
- [ ] Delete resource
- [ ] List resources
- [ ] Resource details page
- [ ] Add tags
- [ ] Track uploader
- [ ] Track upload date

---

### 6. File Upload

Do not store large files directly inside PostgreSQL.

Use object/file storage.

```text
Frontend
    |
    v
Spring Boot
    |
    +----> PostgreSQL
    |        metadata
    |
    +----> Object Storage
             actual file
```

Start with a simple storage provider.

Possible options:

- Cloudflare R2
- AWS S3
- Supabase Storage
- MinIO for local development

- [ ] Upload file
- [ ] Store file URL/key
- [ ] Validate file type
- [ ] Validate file size
- [ ] Generate unique file name
- [ ] Delete file
- [ ] Replace file
- [ ] Handle failed uploads

Initially support:

```text
PDF
DOC
DOCX
PPT
PPTX
XLS
XLSX
ZIP
PNG
JPG
```

Add more only when actually needed.

---

### 7. Resource Approval

Don't let every uploaded file immediately become public.

Flow:

```text
User uploads
      |
      v
   PENDING
      |
      v
    Admin
      |
   +--+--+
   |     |
   v     v
APPROVED REJECTED
   |
   v
PUBLIC
```

- [ ] Add resource status
- [ ] Admin approval page
- [ ] Approve resource
- [ ] Reject resource
- [ ] Delete rejected resources
- [ ] Show uploader the status

---

### 8. Frontend

Build the actual library UI.

#### Home

- [ ] Search bar
- [ ] Recent resources
- [ ] Popular resources
- [ ] Browse by semester
- [ ] Browse by subject

#### Library

```text
Semester
   ↓
Subject
   ↓
Category
   ↓
Resources
```

- [ ] Semester page
- [ ] Subject page
- [ ] Category filters
- [ ] Resource cards
- [ ] Resource details
- [ ] Download button

#### Upload

- [ ] Upload form
- [ ] File picker
- [ ] Title
- [ ] Description
- [ ] Subject
- [ ] Category
- [ ] Tags
- [ ] Upload progress

---

### 9. Search

First make normal search work.

- [ ] Search by title
- [ ] Search by description
- [ ] Search by subject
- [ ] Search by category
- [ ] Search by tags
- [ ] Filter by semester
- [ ] Filter by file type
- [ ] Sort by newest
- [ ] Sort by downloads
- [ ] Pagination

Example:

```text
"operating systems"

        ↓

Operating Systems Notes
OS Assignment 2
OS PYQs
OS Unit 3 Notes
OS Lab Manual
```

Later:

- [ ] PostgreSQL full-text search
- [ ] Better search ranking
- [ ] Search suggestions

Do not add Elasticsearch on day one.

---

### 10. Downloads

- [ ] Download resource
- [ ] Count downloads
- [ ] Download history
- [ ] Show download count
- [ ] Prevent unauthorized downloads

Later:

- [ ] Signed URLs
- [ ] CDN
- [ ] Download analytics

---

### 11. Bookmarks

Let students save resources.

- [ ] Bookmark resource
- [ ] Remove bookmark
- [ ] My bookmarks page
- [ ] Bookmark folders

Example:

```text
My Bookmarks

DSA
├── Arrays Notes
├── Trees Notes
└── Graphs PYQs

End Semester
├── OS PYQs
└── DBMS Notes
```

---

### 12. Reports

Users should be able to report bad resources.

- [ ] Report resource
- [ ] Report reason
- [ ] Admin report list
- [ ] Resolve report
- [ ] Remove reported resource

Reasons:

```text
Wrong resource
Duplicate
Broken file
Wrong subject
Inappropriate
Copyright issue
Other
```

---

### 13. Admin Dashboard

Admin should be able to manage the entire library.

Dashboard:

```text
Users
Resources
Pending uploads
Downloads
Reports
Storage
```

- [ ] User management
- [ ] Resource management
- [ ] Upload approval
- [ ] Report management
- [ ] Department management
- [ ] Semester management
- [ ] Subject management

---

### 14. Duplicate Detection

This is where the SHA-256 thing can actually be useful.

When a file is uploaded:

```text
File
 |
 v
SHA-256
 |
 v
Database
 |
 +-- hash already exists --> duplicate
 |
 +-- new hash ------------> upload
```

- [ ] Generate SHA-256 hash
- [ ] Store hash with file metadata
- [ ] Check hash before upload
- [ ] Reject exact duplicates

Later:

- [ ] Detect similar files
- [ ] Detect different versions of the same resource

---

### 15. File Preview

For supported files:

- [ ] PDF preview
- [ ] Image preview
- [ ] File metadata
- [ ] File size
- [ ] Number of pages for PDFs

Don't build custom document rendering unless there is a reason.

Use existing browser/viewer support where possible.

---

### 16. User Profiles

- [ ] Profile page
- [ ] Uploaded resources
- [ ] Bookmarks
- [ ] Download history
- [ ] Account settings

Later:

- [ ] Contribution statistics
- [ ] Reputation
- [ ] Badges

---

### 17. Notifications

Keep this simple initially.

- [ ] Upload approved
- [ ] Upload rejected
- [ ] Resource reported
- [ ] Admin announcement

Later:

- [ ] Email notifications
- [ ] Discord notifications
- [ ] Push notifications

---

### 18. Backend Improvements

Once the basic application works, start going beyond:

```text
Controller
    ↓
Service
    ↓
Repository
```

Add things that are actually useful:

- [ ] DTO validation
- [ ] Global exception handler
- [ ] Pagination
- [ ] Filtering
- [ ] Sorting
- [ ] Specifications
- [ ] Proper API error responses
- [ ] API versioning
- [ ] Rate limiting
- [ ] Audit logs
- [ ] Background jobs
- [ ] Caching

---

### 19. Caching

Use Redis only where it makes sense.

Potential cache targets:

```text
Popular resources
Subjects
Semesters
Resource metadata
Search results
```

- [ ] Add Redis
- [ ] Cache frequently requested data
- [ ] Cache invalidation
- [ ] Measure before and after

Don't turn every database query into a Redis problem.

---

### 20. Security

- [ ] Validate file extensions
- [ ] Validate MIME types
- [ ] File size limits
- [ ] Authentication checks
- [ ] Authorization checks
- [ ] Secure file access
- [ ] Rate limiting
- [ ] Input validation
- [ ] CORS configuration
- [ ] Secure password storage
- [ ] Protect admin endpoints
- [ ] Do not expose secrets
- [ ] Do not commit storage credentials
- [ ] Add audit logs for admin actions

---

### 21. Testing

#### Backend

- [ ] Service unit tests
- [ ] Repository tests
- [ ] Controller tests
- [ ] Authentication tests
- [ ] File upload tests
- [ ] Integration tests

#### Frontend

- [ ] Component tests
- [ ] API integration tests
- [ ] Upload flow testing
- [ ] Authentication flow testing
- [ ] Mobile testing

---

### 22. Deployment

Backend:

- [ ] Dockerize Spring Boot
- [ ] Production PostgreSQL
- [ ] Production object storage
- [ ] Environment variables
- [ ] Database backups

Frontend:

- [ ] Production build
- [ ] Deploy frontend
- [ ] Configure environment variables

Infrastructure:

- [ ] Domain
- [ ] HTTPS
- [ ] CI/CD
- [ ] GitHub Actions
- [ ] Error monitoring
- [ ] Application logs

---

# MVP

The first version should NOT contain everything above.

Build this:

```text
Login
  ↓
Browse
  ↓
Semester
  ↓
Subject
  ↓
Resource
  ↓
Download
```

And:

```text
User
  ↓
Upload
  ↓
Pending
  ↓
Admin
  ↓
Approve
  ↓
Library
```

### MVP Checklist

- [ ] Spring Boot backend
- [ ] PostgreSQL
- [ ] JWT authentication
- [ ] User / Admin roles
- [ ] Department
- [ ] Semester
- [ ] Subject
- [ ] Resource
- [ ] File upload
- [ ] Object storage
- [ ] Admin approval
- [ ] Browse resources
- [ ] Search
- [ ] Download
- [ ] Basic admin dashboard

That's enough for v1.

---

# v2

After people actually use the MVP:

- [ ] Bookmarks
- [ ] Download history
- [ ] Reports
- [ ] SHA-256 duplicate detection
- [ ] PDF preview
- [ ] Better search
- [ ] User profiles
- [ ] Notifications
- [ ] Analytics
- [ ] Redis caching

---

# v3

Only after the normal library is solid:

- [ ] Full-text search
- [ ] OCR
- [ ] Automatic tagging
- [ ] Similar-resource detection
- [ ] Semantic search
- [ ] AI summaries
- [ ] Recommendation system
- [ ] Contribution/reputation system
- [ ] Mobile app / PWA

---

# Suggested Stack

### Frontend

```text
Next.js
TypeScript
Tailwind CSS
```

### Backend

```text
Spring Boot
Java
Spring Security
Spring Data JPA
Flyway
```

### Database

```text
PostgreSQL
```

### File Storage

```text
S3-compatible object storage
```

### Local Development

```text
Docker
Docker Compose
MinIO
PostgreSQL
```

### Optional Later

```text
Redis
OpenSearch
Vector Database
```

---

# Repository Structure

```text
virtual-library/
│
├── frontend/
│
├── backend/
│
├── docs/
│
├── infrastructure/
│
├── .github/
│   └── workflows/
│
├── docker-compose.yml
├── README.md
└── ROADMAP.md
```

---

# Actual Build Order

```text
1. Repository setup
2. Spring Boot setup
3. PostgreSQL setup
4. Database entities
5. Flyway migrations
6. Authentication
7. Department / Semester / Subject
8. Resource entity
9. File storage
10. Upload API
11. Admin approval
12. Browse API
13. Search API
14. Download API
15. Frontend
16. Admin dashboard
17. Testing
18. Deployment
19. SHA-256 duplicate detection
20. Bookmarks / reports / analytics
```


