# Idlely - AI-Powered Goal Management PWA

## Enhanced Features (November 2025)

### Live Deployment
**Production URL**: https://9gu9c450d8t6.space.minimax.io

### Key Enhancements Implemented

#### 1. Advanced Structured Data Parser
The app now intelligently parses complex academic schedules with category headers:

**Supported Categories**:
- `PH/QUIZ` - Exams and quizzes (appear on Calendar as RED events)
- `TUGAS` - Assignments and homework (appear on Assignments page as todo items)
- `REMEDIAL/SUSULAN/KELAS TAMBAHAN` - Make-up classes and remedials (Calendar as RED events)
- `GOALS` - Personal objectives (Goals page)
- `EVENTS` - Meetings and activities (Calendar as BLUE events)

**Supported Date Formats**:
- Simple dates: `3 Nov`, `26 Nov`, `13 Nov`
- Date ranges: `30-6 Nov` (uses first date: 30 Nov)
- Time details: `3 Nov Jam ke-0` (preserves time information)
- TBD markers: `belum diketahui`, `TBD`, `unknown`
- Month names in English and Indonesian
- Numeric formats: `12/15`, `15-12`

**Example Input**:
```
PH/QUIZ
- Biologi (post test): 3 Nov 
- Kimia: 3 Nov Jam ke-0
- Biologi (Virus): 5 Nov 

TUGAS
- B.Indo (Video Pidato): 30-6 Nov
- English (Online exercise): 6 Nov
- Informatika (Presentasi): 7 Nov 

REMEDIAL
- Biologi (Kel. Tambahan): 3 Nov 
- Sosiologi (Susulan & Remed): 4 Nov
```

#### 2. Smart Parser Logic
- **Auto-Detection**: Automatically detects if input is structured or unstructured
- **Structured Format**: Uses enhanced parser for category-based data
- **Unstructured Format**: Falls back to MiniMax AI for natural language processing
- **Seamless Integration**: Works with both guest mode (localStorage) and authenticated mode (Supabase)

#### 3. Calendar Date-Click Functionality
- Click any date on the calendar to view all events for that day
- Modal displays assignments, exams, goals, and custom events
- Direct navigation to detailed pages (Assignments, Goals)
- Add new events directly to selected dates

#### 4. Mobile-First Design
- Touch-optimized interface with 48px+ touch targets
- Responsive layouts for all screen sizes
- Large, comfortable input areas on mobile
- Swipe gestures for intuitive navigation
- Optimized button sizes and spacing

#### 5. Data Persistence
- **Guest Mode**: localStorage with automatic cleanup
- **Authenticated Mode**: Supabase real-time database
- Cross-session persistence for:
  - Assignments and completion status
  - Goals and progress
  - Calendar events
  - Analytics data
  - Theme customization

#### 6. Discord Nitro-Style Customization
- Simple, aesthetic-focused customization system
- **Free Features**: All core productivity tools
- **Premium Features**: Visual themes and customization
- **Gradient Themes**: Two-color gradients with live preview
- **Layout Templates**: Default, Dashboard-focused, Compact, Spacious
- **Theme Export/Import**: Save and share custom themes

## Technology Stack

### Frontend
- **React 18** with TypeScript
- **Vite** for build tooling
- **Tailwind CSS** for styling
- **Shadcn/UI** component library
- **React Router** for navigation
- **React Big Calendar** for calendar views

### Backend
- **Supabase** for database and authentication
- **MiniMax AI** for intelligent text parsing
- **Edge Functions** for serverless processing

### Features
- **PWA** (Progressive Web App) with offline support
- **Real-time Sync** across devices
- **Multilingual Support** (12 languages including Indonesian)
- **Smart Notifications** with deadline reminders
- **Analytics Dashboard** with progress tracking

## Getting Started

### Prerequisites
- Node.js 18+ and pnpm
- Supabase account (for backend)
- MiniMax AI API key (for AI parsing)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/aceteria/idlely.git
   cd idlely
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

3. **Configure environment variables**
   
   Create `.env.local` file:
   ```env
   VITE_SUPABASE_URL=your_supabase_url
   VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
   VITE_MINIMAX_API_KEY=your_minimax_api_key
   VITE_MINIMAX_GROUP_ID=your_minimax_group_id
   ```

4. **Run development server**
   ```bash
   pnpm dev
   ```

5. **Build for production**
   ```bash
   pnpm build
   ```

### Supabase Setup

1. **Create Supabase project** at https://supabase.com

2. **Run migrations** (in `supabase/migrations/` directory)
   ```bash
   supabase db push
   ```

3. **Configure authentication**
   - Enable Email authentication
   - Set up OAuth providers (optional)

4. **Set up Row Level Security (RLS)**
   - Policies are included in migration files
   - Verify policies are enabled in Supabase dashboard

## Project Structure

```
idlely-mvp/
├── src/
│   ├── components/         # Reusable UI components
│   ├── contexts/          # React contexts (Auth, Theme, etc.)
│   ├── pages/            # Page components
│   ├── services/         # API and business logic
│   ├── utils/            # Utility functions
│   │   └── enhanced-parser.ts  # NEW: Structured data parser
│   └── lib/              # Third-party integrations
├── supabase/
│   ├── migrations/       # Database migrations
│   └── functions/        # Edge functions
├── public/              # Static assets
└── dist/               # Production build
```

## Key Files

### Enhanced Parser
- **File**: `src/utils/enhanced-parser.ts`
- **Purpose**: Parses structured academic schedules
- **Usage**: Auto-imported in InboxPage.tsx

### InboxPage Integration
- **File**: `src/pages/InboxPage.tsx`
- **Enhancement**: Lines 766-850 (structured parser integration)
- **Logic**: 
  1. Try enhanced parser first
  2. If structured format detected, use it
  3. Otherwise, fall back to MiniMax AI

## Testing

### Manual Testing

1. **Navigate to Smart Inbox**
2. **Paste structured data** (see example above)
3. **Click "Process Message"**
4. **Verify categorization**:
   - Assignments page shows TUGAS items
   - Calendar shows PH/QUIZ and REMEDIAL as RED events
5. **Test calendar date-click**:
   - Click on any date with events
   - Modal should show all events for that date
6. **Test mobile responsiveness**:
   - Open in mobile browser or DevTools mobile view
   - Verify touch targets and layouts

### Test Account
- **Email**: test1@idlelyapp.com
- **Password**: TestAccount123!
- **Premium Key**: IDLELYPREMIUM2025A1

## Deployment

### Vercel/Netlify
1. Connect GitHub repository
2. Set environment variables
3. Deploy

### Manual Deployment
```bash
pnpm build
# Upload dist/ folder to your hosting service
```

### Docker (Optional)
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN npm install -g pnpm && pnpm install --frozen-lockfile
COPY . .
RUN pnpm build
EXPOSE 3000
CMD ["pnpm", "preview"]
```

## Contributing

### Development Workflow
1. Create feature branch: `git checkout -b feature/your-feature`
2. Make changes and test locally
3. Commit with clear messages: `git commit -m "feat: add feature"`
4. Push and create pull request

### Code Style
- TypeScript strict mode
- ESLint for linting
- Prettier for formatting (auto on save)

## Known Issues & Limitations

### Current Limitations
- Enhanced parser currently supports Indonesian and English date formats
- Maximum localStorage size: ~5MB for guest mode
- Calendar events limited to 1000 per user (Supabase tier dependent)

### Planned Features
- Additional language support for date parsing
- Bulk import/export for assignments
- Collaborative goal tracking
- Integration with Google Calendar
- Native mobile apps (iOS/Android)

## License

This project is for educational purposes. All rights reserved.

## Contact & Support

- **GitHub**: https://github.com/aceteria/idlely
- **Issues**: Report bugs via GitHub Issues
- **Email**: support@idlelyapp.com (for sensitive issues)

## Acknowledgments

- **MiniMax AI** for intelligent text parsing
- **Supabase** for backend infrastructure
- **Shadcn/UI** for beautiful components
- **Open source community** for inspiration and tools

## Changelog

### Version 2.0 (November 2025)
- ✨ **NEW**: Enhanced structured data parser
- ✨ **NEW**: Support for category-based academic schedules
- ✨ **NEW**: Indonesian date format parsing
- ✨ **NEW**: TBD/belum diketahui handling
- ✨ **NEW**: Time detail preservation (Jam ke-X)
- ✨ **NEW**: Date range support (30-6 Nov)
- 🎨 **IMPROVED**: Mobile-first responsive design
- 🎨 **IMPROVED**: Calendar date-click functionality
- 🎨 **IMPROVED**: Data persistence across sessions
- 🐛 **FIXED**: Various UI/UX improvements

### Version 1.0 (October 2025)
- 🎉 Initial release
- Basic assignment and goal tracking
- AI-powered text parsing
- Calendar integration
- Analytics dashboard
- PWA support

---

**Built with ❤️ for students by students**