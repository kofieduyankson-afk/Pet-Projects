Frontend: Next.js + React + TypeScript
Database: PostgreSQL
ORM: Prisma
Authentication: NextAuth/Auth.js or your existing auth solution
Canvas: React Flow (excellent for draggable node-based UIs) or a combination of React Konva and D3.js for more custom control
Styling: Tailwind CSS
Real-time collaboration (optional): WebSockets or Liveblocks
File storage: Cloudinary, S3, or local storage during development


Architecture
src/
├── app/
├── components/
│   ├── board/
│   ├── timeline/
│   ├── graph/
│   ├── person/
│   ├── project/
│   └── relationships/
├── lib/
│   ├── graph/
│   ├── prisma/
│   └── services/
├── prisma/
│   └── schema.prisma
└── types/
