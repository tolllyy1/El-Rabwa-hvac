# El-Rabwa HVAC Management System

A production-ready HVAC CRM & Management System built with Next.js, React, TypeScript, and Supabase.

## Features

✅ **Dashboard** - Real-time metrics and overview
✅ **Customer Management** - Add and manage customers
✅ **Jobs Tracking** - Track all service calls and installations
✅ **Invoicing** - Create and manage invoices
✅ **Calendar View** - Visual scheduling
✅ **Dark/Light Theme** - Complete theme support
✅ **Responsive Design** - Mobile-friendly interface

## Quick Start

### Prerequisites
- Node.js 18+
- npm or yarn
- Supabase account (free at supabase.com)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/tolllyy1/El-Rabwa-hvac.git
   cd El-Rabwa-hvac
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up Supabase**
   - Go to https://supabase.com and create a new project
   - Get your Project URL and Anon Key from Settings > API
   - Create `.env.local` in the root directory:
     ```
     NEXT_PUBLIC_SUPABASE_URL=https://tpimzmfxdhhksunkfknl.supabase.co
     NEXT_PUBLIC_SUPABASE_ANON_KEY=sb_publishable_SLwGOhQb4qDPv1jjrb0lSA_Jev3_nm3
     ```

4. **Initialize Database**
   - Go to SQL Editor in Supabase
   - Run the following SQL:

   ```sql
   -- Create customers table
   CREATE TABLE customers (
     id BIGSERIAL PRIMARY KEY,
     name VARCHAR(255) NOT NULL,
     email VARCHAR(255),
     phone VARCHAR(20),
     address TEXT,
     city VARCHAR(100),
     created_at TIMESTAMP DEFAULT NOW(),
     updated_at TIMESTAMP DEFAULT NOW()
   );

   -- Create jobs table
   CREATE TABLE jobs (
     id BIGSERIAL PRIMARY KEY,
     customer_id BIGINT NOT NULL REFERENCES customers(id) ON DELETE CASCADE,
     job_type VARCHAR(100),
     status VARCHAR(50) DEFAULT 'pending',
     description TEXT,
     scheduled_date DATE,
     completed_date DATE,
     total_amount DECIMAL(10, 2),
     created_at TIMESTAMP DEFAULT NOW(),
     updated_at TIMESTAMP DEFAULT NOW()
   );

   -- Create invoices table
   CREATE TABLE invoices (
     id BIGSERIAL PRIMARY KEY,
     job_id BIGINT NOT NULL REFERENCES jobs(id) ON DELETE CASCADE,
     customer_id BIGINT NOT NULL REFERENCES customers(id) ON DELETE CASCADE,
     invoice_number VARCHAR(50) UNIQUE,
     amount DECIMAL(10, 2) NOT NULL,
     status VARCHAR(50) DEFAULT 'pending',
     due_date DATE,
     paid_date DATE,
     created_at TIMESTAMP DEFAULT NOW(),
     updated_at TIMESTAMP DEFAULT NOW()
   );
   ```

5. **Run locally**
   ```bash
   npm run dev
   ```
   Open http://localhost:3000

## Project Structure

```
src/
├── app/
│   ├── page.tsx              # Dashboard
│   ├── customers/            # Customers module
│   ├── jobs/                 # Jobs module
│   ├── invoices/             # Invoices module
│   ├── calendar/             # Calendar view
│   ├── layout.tsx            # Root layout
│   └── globals.css           # Global styles
├── components/
│   ├── navbar.tsx            # Navigation
│   ├── theme-provider.tsx    # Theme management
│   └── dashboard-card.tsx    # Dashboard card component
└── lib/
    └── supabase.ts           # Supabase client
```

## Customization

### Adding Your Logo
1. Place your logo in `public/logo.png`
2. Update `src/components/navbar.tsx` (line ~8) to use your logo

### Changing Colors
- Edit `tailwind.config.ts` to customize the color scheme
- Current colors: White background + Dark Blue accents

### Adding Dark/Light Theme Toggle
- Already implemented! Toggle is in the navbar (top right)

## Deployment

### Deploy to Vercel (Recommended)
1. Push to GitHub
2. Go to https://vercel.com
3. Import your repository
4. Add environment variables (Supabase URL and Key)
5. Deploy!

## Next Steps (Phase 2)

- [ ] Installment plans for invoices
- [ ] Collections tracking
- [ ] Sales targets
- [ ] Attachments per job
- [ ] Advanced reporting
- [ ] Mobile app

## Support

For issues or questions, please create a GitHub issue.

## License

MIT
