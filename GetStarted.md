#Create project
npx create-next-app@latest crumpet-board
#selet
✔ TypeScript → Yes
✔ ESLint → Yes
✔ Tailwind CSS → Yes
✔ src/ directory → Yes
✔ App Router → Yes
✔ Turbopack → Yes
✔ Import Alias → Yes (@/*)
#GIT INITIALIZATION
git init
git add .
git commit -m "Initial Next.js project"

#INSTALL DEPENDACIES
npm install prisma @prisma/client
npm install zod
npm install react-hook-form
npm install axios
npm install clsx
npm install date-fns
npm install uuid
npm install bcryptjs
npm install jsonwebtoken
#UI LIBARIES
npm install lucide-react
npm install reactflow
npm install framer-motion
npm install sonner
npm install recharts
#drag and drop
npm install @dnd-kit/core
npm install @dnd-kit/sortable

#INITIALISE PRISMA
npx prisma init
in env DATABASE_URL="postgresql://postgres:password@localhost:5432/crumpet_board"
createdb crumpet_board
npx prisma migrate dev --name init
npx prisma generate
npx prisma studio

#UI COMPONENETS TO USE
npx shadcn@latest init
npx shadcn@latest add button
npx shadcn@latest add card
npx shadcn@latest add input
npx shadcn@latest add textarea
npx shadcn@latest add dialog
npx shadcn@latest add dropdown-menu
npx shadcn@latest add popover
npx shadcn@latest add command
npx shadcn@latest add sheet
npx shadcn@latest add tabs
npx shadcn@latest add badge
npx shadcn@latest add avatar
npx shadcn@latest add tooltip
npx shadcn@latest add separator
npx shadcn@latest add scroll-area


#FOLDER STRUCTURE
mkdir -p src/components
mkdir -p src/components/ui
mkdir -p src/components/board
mkdir -p src/components/layout
mkdir -p src/components/person
mkdir -p src/components/project
mkdir -p src/components/relationship

mkdir -p src/lib
mkdir -p src/lib/actions
mkdir -p src/lib/prisma
mkdir -p src/lib/utils

mkdir -p src/hooks

mkdir -p src/types

mkdir -p src/services

mkdir -p src/constants

mkdir -p src/data
