# 🎬 ScreenSphere 

A modern movie discovery and favorites platform built with Next.js 15, Supabase, and TMDB API.

## ✨ Features

- 🎭 **Movie Discovery**: Browse trending, popular, and upcoming movies
- 🔍 **Real-time Search**: Search movies with instant results and release years
- ❤️ **Favorites System**: Save and manage your favorite movies
- 👤 **User Authentication**: Secure sign-up/sign-in with email confirmation
- 📱 **Responsive Design**: Beautiful dark theme that works on all devices
- 🐳 **Docker Ready**: One-command deployment with Docker Compose

## 🚀 Quick Start

### Prerequisites
- Node.js 18.17+
- TMDB API key ([Get one here](https://www.themoviedb.org/settings/api))
- Supabase project ([Create one here](https://supabase.com))

### 1. Clone and Install
```bash
git clone https://github.com/arfadex/screensphere.git
cd screensphere
npm install
```

### 2. Environment Setup
Create `.env.local`:
```bash
TMDB_API_KEY=your_tmdb_api_key_here
AUTH_SECRET=your_auth_secret
NEXT_PUBLIC_SUPABASE_URL=https://your-project-id.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key_here
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key_here
```

### 3. Database Setup
Run this SQL in your Supabase SQL Editor:
```sql
CREATE TABLE IF NOT EXISTS public.favorites (
    id UUID DEFAULT uuid_generate_v4() PRIMARY KEY,
    user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
    tmdb_id INTEGER NOT NULL,
    title TEXT,
    overview TEXT,
    poster_path TEXT,
    status TEXT,
    release_date DATE DEFAULT '1900-01-01',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    UNIQUE(user_id, tmdb_id)
);

ALTER TABLE public.favorites ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Users can manage their own favorites" ON public.favorites
    FOR ALL USING (auth.uid() = user_id);
```

### 4. Run the App
```bash
npm run dev
```
Visit [http://localhost:3000](http://localhost:3000)

## 🐳 Docker Deployment

```bash
# Quick start with Docker
docker-compose up --build

# Access at http://localhost:3000
```

## 📄 License

This project is licensed under the GNU General Public License.

---

**⭐ Star this repository if you found it helpful!**