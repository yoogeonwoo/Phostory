# Phostory Product Specification & Structure Log

This document provides a comprehensive overview of the Phostory web application's current architecture, features, and technical specifications. It is designed to serve as a complete reference for any future development or debugging.

---

## 1. Project Architecture
Phostory is a modern Single Page Application (SPA) built with a minimalist, high-performance approach.

- **Frontend**: Vanilla HTML5, CSS3, and JavaScript (ES Modules).
- **Backend Services**: Supabase (PostgreSQL, Auth, Storage).
- **Design Philosophy**: Glassmorphism, premium typography (Outfit), and responsive masonry layouts.

---

## 2. File Structure
- `index.html`: The structural backbone containing all view containers (Home, About, Make, Share, Profile, Settings) and the application logic (inline script).
- `style.css`: The central design system containing glassmorphism effects, responsive grid logic, and micro-animations.
- `DEVELOPMENT_LOG.md`: Historical record of session changes.
- `STRUCTURE_LOG.md`: This document (Technical & Functional reference).

---

## 3. UI/UX Map (Views)
The application dynamically switches between views using a `switchView()` system.

### A. Navigation & Header
- **Logo**: Clicking returns user to Home.
- **Hamburger Menu**: Dropdown navigation for all features.

### B. Home View (`#homeView`)
- **Discovery Grid**: Infinite/Masonry layout for public photos.
- **Filter Chips**: 
    - `All Stories`: Default public view.
    - `My Likes`: Posts the current user has liked.
    - `Top Liked`: (Placeholder) Aimed at trending content.

### C. About Us View (`#aboutView`)
- Brand story and mission statement for Phostory.

### D. Make My Phostory (`#makeView`)
- **Upload Form**: Title, Image upload (drag/drop), Visibility toggle (Public/Private).
- **My Uploads List**: Mini masonry grid to manage personal posts (Edit/Delete).

### E. Share My Phostory (`#shareView`)
- **Profile Link**: Generated unique URL (`?user=username`) for sharing.
- **Profile Customization**: Bio editing and Avatar upload.
- **Public Preview**: Real-time mockup of how others see the profile.

### G. Settings View (`#settingsView`)
- **Account Management**: Update @ID (username), Change Password.
- **Danger Zone**: Permanent account deletion.

### H. Public Profile View (`#profilePageView`)
- Dynamic view triggered by `?user=` URL parameter. Displays public/private posts depending on access.

---

## 4. Feature Specifications

### 🔑 Authentication
- **ID-Based Login**: Users can sign up and sign in using a unique @username or email.
- **Real-time Check**: Automatically checks if a username is available during signup.

### 🖼️ Content Management
- **Masonry Grid**: Responsive multi-column layout that scales horizontally (2 to 6+ columns).
- **Visibility Control**: 
    - `Public`: Visible on the main home discovery grid.
    - `Private`: Visible only on the user's profile/share link.
- **Post Interaction**: Like/Unlike persistent states saved to DB.
- **Edit/Delete**: Complete CRUD functionality for user posts.

### 📱 Mobile Optimization
- **Responsive Design**: Adapts from mobile (2 columns) to desktop (multi-column).
- **Touch Interaction**: Photo cards reveal metadata (Title, Author, Like) on tap.

---

## 5. Backend & Database Schema (Supabase)

### 📊 Tables
- **`profiles`**:
    - `id` (UUID, primary key)
    - `username` (Text, unique)
    - `email` (Text)
    - `bio` (Text)
    - `avatar_url` (Text)
- **`posts`**:
    - `id` (BigInt, primary key)
    - `user_id` (UUID, FK to profiles)
    - `title` (Text)
    - `image_url` (Text)
    - `is_public` (Boolean)
    - `created_at` (Timestamp)
- **`likes`**:
    - `id` (BigInt, primary key)
    - `user_id` (UUID)
    - `post_id` (BigInt)

### 📁 Storage Buckets
- `public_photos`: Storage for posts set to public visibility.
- `private_photos`: Storage for posts set to private visibility.
- `profiles`: Storage for user avatar images.

---

## 6. Technical Configuration
- **Supabase URL**: `https://jlxlccrhwmmrubvgyloi.supabase.co`
- **Supabase Key**: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...` (Anon Key)
- **External Assets**:
    - Google Fonts: `Outfit` (300, 600)
    - Dummy Images: `picsum.photos`
    - Dummy Avatars: `pravatar.cc`
