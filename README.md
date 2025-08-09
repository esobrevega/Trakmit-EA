This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

# Trakmit-EA
[![Ask DeepWiki](https://devin.ai/assets/askdeepwiki.png)](https://deepwiki.com/esobrevega/Trakmit-EA)

Trakmit-EA (Permitrakk) is a comprehensive, full-stack project and permit management system. Built with a modern technology stack including Next.js, Appwrite, and Hono, it provides a collaborative platform for teams to manage workspaces, projects, and permits (tasks) efficiently. The application features a modular, feature-sliced architecture for maintainability and scalability.

## ✨ Key Features

-   **User Authentication**: Secure sign-up, sign-in, and session management powered by Appwrite.
-   **Workspace Management**: Create, switch between, and manage multiple workspaces. Each workspace has its own members, projects, and settings.
-   **Project Management**: Organize work into projects within a workspace. Each project has a dedicated dashboard, settings, and analytics.
-   **Permit (Task) Management**: Create, update, and track permits with various statuses. View permits in multiple formats:
    -   **Table View**: A sortable and searchable data grid for all permits.
    -   **Kanban Board**: A drag-and-drop interface to manage permit status (`Backlog`, `To Do`, `In Progress`, `In Review`, `Done`).
    -   **Calendar View**: A monthly calendar to visualize permit due dates.
-   **Member & Role Management**: Invite new members to a workspace via a unique, shareable link. Assign roles (`Admin`, `Member`) to manage permissions.
-   **Analytics**: Dashboards for both workspaces and projects, providing insights into permit statistics (total, completed, overdue, etc.).
-   **Responsive UI**: A modern and sleek interface built with Tailwind CSS and shadcn/ui, optimized for both desktop and mobile devices.

## 🛠️ Technology Stack

-   **Framework**: [Next.js](https://nextjs.org/) (App Router)
-   **Backend-as-a-Service**: [Appwrite](https://appwrite.io/) (Database, Authentication, Storage)
-   **API Layer**: [Hono](https://hono.dev/) (for lightweight, type-safe API routes)
-   **Styling**: [Tailwind CSS](https://tailwindcss.com/) & [shadcn/ui](https://ui.shadcn.com/)
-   **Data-Fetching & State**: [TanStack Query](https://tanstack.com/query/latest)
-   **Form Handling**: [React Hook Form](https://react-hook-form.com/) & [Zod](https://zod.dev/)
-   **Language**: [TypeScript](https://www.typescriptlang.org/)
-   **UI Components**: [Recharts](https://recharts.org/) (Charts), [React Big Calendar](http://jquense.github.io/react-big-calendar/), `@hello-pangea/dnd` (Kanban)

## 🚀 Getting Started

Follow these instructions to set up and run the project locally.

### Prerequisites

-   Node.js (v20 or newer)
-   npm, yarn, or pnpm
-   An Appwrite instance (can be self-hosted via Docker or on [Appwrite Cloud](https://cloud.appwrite.io/))

### Appwrite Setup

1.  Create a new Appwrite Project.
2.  **Database**:
    -   Create a new Database. Note its ID.
    -   Create the following collections and note their IDs:
        -   `workspaces`
        -   `projects`
        -   `tasks`
        -   `members`
3.  **Authentication**: Enable the **Email/Password** provider in the Auth section.
4.  **Storage**: Create a new Storage Bucket named `images` (or similar) and note its ID.
5.  **API Keys**: In your Project Settings, go to the **API Keys** tab and create a new API Key with `databases`, `users`, and `storage` scopes. Note the secret key.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/esobrevega/trakmit-ea.git
    cd trakmit-ea
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Set up environment variables:**
    Create a `.env.local` file in the project root and add your Appwrite credentials.

    ```env
    # Appwrite Configuration
    NEXT_PUBLIC_APPWRITE_ENDPOINT=https://cloud.appwrite.io/v1
    NEXT_PUBLIC_APPWRITE_PROJECT=YOUR_PROJECT_ID
    NEXT_APPWRITE_KEY=YOUR_SERVER_API_KEY

    # Appwrite Database & Collection IDs
    NEXT_PUBLIC_APPWRITE_DATABASE_ID=YOUR_DATABASE_ID
    NEXT_PUBLIC_APPWRITE_WORKSPACES_ID=YOUR_WORKSPACES_COLLECTION_ID
    NEXT_PUBLIC_APPWRITE_MEMBERS_ID=YOUR_MEMBERS_COLLECTION_ID
    NEXT_PUBLIC_APPWRITE_PROJECTS_ID=YOUR_PROJECTS_COLLECTION_ID
    NEXT_PUBLIC_APPWRITE_TASKS_ID=YOUR_TASKS_COLLECTION_ID

    # Appwrite Storage Bucket ID
    NEXT_PUBLIC_APPWRITE_IMAGES_BUCKET_ID=YOUR_IMAGES_BUCKET_ID

    # Application URL
    NEXT_PUBLIC_APP_URL=http://localhost:3000
    ```

4.  **Run the development server:**
    ```bash
    npm run dev
    ```

The application will be available at `http://localhost:3000`.

## 📂 Project Structure

The project utilizes a feature-sliced design to maintain organization and promote scalability.

```
src
├── app/                  # Next.js App Router: Layouts, Pages, and API routes
│   ├── (auth)/           # Routes for authentication (sign-in, sign-up)
│   ├── (dashboard)/      # Protected routes for the main application dashboard
│   ├── (standalone)/     # Pages with a minimal layout (e.g., settings, invites)
│   └── api/[[...route]]/ # Hono API endpoint for backend logic
├── components/           # Shared, reusable UI components (built with shadcn/ui)
├── features/             # Business logic modules, sliced by feature
│   ├── auth/             # Authentication logic, hooks, and components
│   ├── members/          # Member management logic
│   ├── projects/         # Project management logic
│   ├── tasks/            # Permit/Task management logic
│   └── workspaces/       # Workspace management logic
├── hooks/                # Global custom React hooks
└── lib/                  # Core utilities and configurations (Appwrite, Hono RPC)
```

## 🌐 API Endpoints

The backend is built with Hono and exposed through a single Next.js dynamic route at `/api`. Hono's RPC mode allows for type-safe communication between the client and server.

-   `/api/auth`: Handles user registration, login, logout, and session management.
-   `/api/workspaces`: CRUD for workspaces, member invites, and analytics.
-   `/api/projects`: CRUD for projects and project-specific analytics.
-   `/api/tasks`: CRUD for permits (tasks), including bulk updates for Kanban board interactions.
-   `/api/members`: Manages fetching, updating, and removing workspace members.
