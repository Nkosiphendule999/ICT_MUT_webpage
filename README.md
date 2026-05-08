# ICT_MUT_webpage
updated version of MUT ICT webpage 
# MUT ICT Department Webpage

A comprehensive web application for the Mangosuthu University of Technology - Department of Information & Communication Technology. This system provides student registration, login, consultation booking, peer support, and contact management features with Supabase backend integration.

## 📋 Table of Contents
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Database Setup](#database-setup)
- [Configuration](#configuration)
- [Running the Project](#running-the-project)
- [Project Structure](#project-structure)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

- **User Authentication** - Student and External user registration/login
- **Consultation Booking** - Schedule appointments with lecturers
- **Peer Support Program** - Request mentorship and academic support
- **Contact Management** - Store contact messages in database
- **AI Chatbot** - 24/7 virtual assistant for common queries
- **FAQ Section** - Expandable frequently asked questions
- **Responsive Design** - Works on desktop, tablet, and mobile devices

## 🛠 Tech Stack

| Technology | Purpose |
|------------|---------|
| HTML5 | Structure and content |
| CSS3 | Styling and animations |
| JavaScript (ES6) | Client-side logic and interactivity |
| Supabase | Backend database and authentication |
| Font Awesome | Icons and visual elements |
| Google Fonts | Typography |

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

1. **Visual Studio Code** - [Download](https://code.visualstudio.com/)
2. **Live Server Extension** - Install from VS Code Extensions Marketplace
3. **Supabase Account** - [Sign up for free](https://supabase.com/)

## 💻 Installation

### Step 1: Clone or Download the Project

```bash
# If using Git
git clone https://github.com/your-username/mut-ict-website.git

Install Live Server Extension
1. Open VS Code
2. Click on Extensions icon (Ctrl+Shift+X)
3. Search for "Live Server"
4. Click Install on "Live Server" by Ritwick Dey
5. Wait for installation to complete


Supabase sql table creation :
-- Create users table
CREATE TABLE IF NOT EXISTS public.users (
    user_id SERIAL PRIMARY KEY,
    user_type VARCHAR(20) NOT NULL CHECK (user_type IN ('student', 'external')),
    student_number VARCHAR(8) UNIQUE NULL,
    username VARCHAR(50) NOT NULL UNIQUE,
    first_name VARCHAR(50) NOT NULL,
    surname VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone_number VARCHAR(10) NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create student_details table
CREATE TABLE IF NOT EXISTS public.student_details (
    detail_id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL REFERENCES users(user_id) ON DELETE CASCADE,
    student_number VARCHAR(8) NOT NULL UNIQUE,
    year_of_study VARCHAR(50) DEFAULT '1st Year',
    faculty VARCHAR(100),
    department VARCHAR(100),
    registration_status VARCHAR(20) DEFAULT 'pending'
);

-- Create external_details table
CREATE TABLE IF NOT EXISTS public.external_details (
    detail_id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL REFERENCES users(user_id) ON DELETE CASCADE,
    organization VARCHAR(100),
    position VARCHAR(100),
    interests TEXT,
    referral_source VARCHAR(100),
    newsletter_subscribed BOOLEAN DEFAULT FALSE
);

-- Create consultations table
CREATE TABLE IF NOT EXISTS public.consultations (
    consultation_id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL REFERENCES users(user_id) ON DELETE CASCADE,
    lecturer_name VARCHAR(100) NOT NULL,
    consultation_date DATE NOT NULL,
    consultation_time TIME NOT NULL,
    module VARCHAR(100),
    reason TEXT,
    status VARCHAR(20) DEFAULT 'pending',
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create contact_messages table
CREATE TABLE IF NOT EXISTS public.contact_messages (
    message_id SERIAL PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    student_number VARCHAR(20),
    message TEXT NOT NULL,
    status VARCHAR(20) DEFAULT 'unread',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create peer_support_requests table
CREATE TABLE IF NOT EXISTS public.peer_support_requests (
    request_id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL REFERENCES users(user_id) ON DELETE CASCADE,
    full_name VARCHAR(100) NOT NULL,
    student_id VARCHAR(50) NOT NULL,
    year_of_study VARCHAR(50),
    support_area VARCHAR(100),
    notes TEXT,
    status VARCHAR(20) DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Enable Row Level Security
ALTER TABLE public.users ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.student_details ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.external_details ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.consultations ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.contact_messages ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.peer_support_requests ENABLE ROW LEVEL SECURITY;

-- Create policies for development (allow all operations)
CREATE POLICY "Allow all operations" ON public.users FOR ALL USING (true);
CREATE POLICY "Allow all operations" ON public.student_details FOR ALL USING (true);
CREATE POLICY "Allow all operations" ON public.external_details FOR ALL USING (true);
CREATE POLICY "Allow all operations" ON public.consultations FOR ALL USING (true);
CREATE POLICY "Allow all operations" ON public.contact_messages FOR ALL USING (true);
CREATE POLICY "Allow all operations" ON public.peer_support_requests FOR ALL USING (true);

🔧 Configuration
Step 1: Update Supabase Credentials
You need to update the Supabase configuration in each HTML file. Open each file and find this section:

javascript
// Find this code in each file
const SUPABASE_URL = 'https://your-project-id.supabase.co';
const SUPABASE_ANON_KEY = 'your-anon-key-here';
Files to update:

register.html

login.html

consultation.html

contact.html

Replace with your actual credentials:

javascript
const SUPABASE_URL = 'https://abcdefg.supabase.co';  // Your Project URL
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIs...';  // Your anon key

# Or download the ZIP file and extract it
