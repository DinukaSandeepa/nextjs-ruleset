# Next.js Project Ruleset and Folder Structure

This document outlines the ruleset and folder structure for a Next.js project using MongoDB, JavaScript, and shadcn/ui. The guidelines aim to ensure scalability, maintainability, and consistency across the team, addressing issues like component bloat, disorganized structure, and naming inconsistencies.

> **🚀 Quick Start**: Use our official starter template: `npx create-next-shadcn-mongo my-app`  
> This template implements all the rules and structure outlined in this document.

## 1. Project Setup Rules

- **Next.js Version**: Use the latest stable version of Next.js (e.g., 15.x or higher) with the App Router for better scalability and performance.
- **Language**: Use JavaScript (ES Modules) for consistency. Avoid mixing JavaScript and TypeScript unless the team explicitly adopts TypeScript.
- **Dependencies**:
  - Use `shadcn/ui` for UI components to ensure customizable, accessible, and lightweight components.
  - Use `mongoose` for MongoDB interactions to simplify schema creation and data modeling.
  - Use `next-auth` or similar for authentication, if required.
  - Use `axios` or `fetch` for API calls, with a preference for `fetch` for simplicity unless complex request handling is needed.
- **Tooling**:
  - Use ESLint and Prettier for code linting and formatting. Configure with Next.js defaults and add custom rules for consistency (e.g., single quotes, trailing commas).
  - Use a `.env.local` file for environment variables (e.g., MongoDB URI, API keys).
- **Version Control**: Use Git with a clear branching strategy (e.g., Gitflow). Enforce pull requests with code reviews.
- ![Logo](./assets/HotfixBranches.svg)


## 2. Folder Structure

The folder structure is designed to be modular, scalable, and aligned with Next.js App Router conventions. Below is the recommended structure:

```
/project-root
├── /app
│   ├── /api
│   │   ├── /auth
│   │   │   └── [...nextauth].js        # NextAuth configuration
│   │   ├── /users
│   │   │   └── route.js               # API route for user-related operations
│   │   └── /products
│   │       └── route.js               # API route for product-related operations
│   ├── /dashboard
│   │   ├── page.jsx                    # Dashboard page
│   │   ├── layout.jsx                  # Dashboard-specific layout
│   │   └── /_components                # Page-specific components
│   ├── /auth
│   │   ├── /login
│   │   │   └── page.jsx                # Login page
│   │   └── /register
│   │       └── page.jsx                # Register page
│   ├── page.jsx                       # Root page (e.g., homepage)
│   ├── layout.jsx                      # Root layout
│   └── globals.css                    # Global styles (Tailwind + shadcn/ui)
├── /components
│   ├── /ui                            # shadcn/ui components
│   │   ├── button.jsx                  # Reusable Button component
│   │   ├── input.jsx                   # Reusable Input component
│   │   └── ...                        # Other shadcn/ui components
│   ├── /common                        # Reusable, non-page-specific components
│   │   ├── header.jsx                  # Header component
│   │   ├── footer.jsx                  # Footer component
│   │   └── navbar.jsx                  # Navigation bar
│   └── /feature                       # Feature-specific components
│       ├── /user
│       │   ├── user-profile.jsx        # User profile component
│       │   └── user-list.jsx           # User list component
│       └── /product
│           ├── product-card.jsx        # Product card component
│           └── product-form.jsx        # Product form component
├── /lib
│   ├── /db
│   │   └── mongoose.js                # MongoDB connection setup
│   ├── /models
│   │   ├── user.js                    # Mongoose User schema
│   │   └── product.js                 # Mongoose Product schema
│   ├── /utils
│   │   ├── api.js                     # API utility functions (e.g., fetch wrappers)
│   │   └── formatters.js              # Formatting utilities (e.g., date, currency)
│   └── /hooks
│       ├── use-auth.js                # Custom hook for authentication
│       └── use-products.js            # Custom hook for product data
├── /public
│   ├── /images                        # Static images
│   ├── /fonts                         # Custom fonts (if any)
│   └── favicon.ico                    # Favicon
├── /styles
│   └── tailwind.css                   # Tailwind CSS configuration
├── /tests
│   ├── /unit                          # Unit tests
│   ├── /integration                   # Integration tests
│   └── /e2e                           # End-to-end tests
├── .env.local                         # Environment variables
├── .eslintrc.json                     # ESLint configuration
├── .prettierrc                        # Prettier configuration
├── next.config.js                     # Next.js configuration
├── package.json                       # Project dependencies
├── README.md                          # Project documentation
└── tailwind.config.js                 # Tailwind configuration
```

### Explanation of Folder Structure

- **/app**: Contains all pages, layouts, and API routes per Next.js App Router conventions. Group related pages (e.g., `/dashboard`, `/auth`) for better organization.
- **/components**: Organized into `/ui` (shadcn/ui components), `/common` (global reusable components), and `/feature` (feature-specific components) to avoid clutter.
- **/lib**: Stores database connections, models, utilities, and custom hooks for reusability and separation of concerns.
- **/public**: Static assets like images and fonts.
- **/styles**: Tailwind CSS configuration for styling, integrated with shadcn/ui.
- **/tests**: Organized by test type for unit, integration, and end-to-end testing.

## 3. Naming Conventions

Consistent naming improves readability and collaboration. Follow these rules:

- **Files and Folders**:
  - Use **kebab-case** for file and folder names (e.g., `user-profile.js`, `product-card.js`).
  - Use lowercase for all files and folders.
  - Name API routes and pages according to their purpose (e.g., `users/route.js`, `login/page.js`).
- **Components**:
  - Use **PascalCase** for component names (e.g., `UserProfile`, `ProductCard`).
  - Prefix shadcn/ui components with `Ui` for clarity (e.g., `UiButton`, `UiInput`).
- **Functions and Variables**:
  - Use **camelCase** for functions and variables (e.g., `fetchUserData`, `userId`).
  - Use descriptive names that reflect purpose (e.g., `formatCurrency` instead of `format`).
- **MongoDB Models**:
  - Use **PascalCase** for Mongoose model names (e.g., `User`, `Product`).
  - Use singular names for models (e.g., `User` instead of `Users`).
- **API Routes**:
  - Use RESTful naming conventions (e.g., `/api/users` for user-related endpoints).
  - Use HTTP methods in `route.js` (e.g., `GET`, `POST`) for clarity.

## 4. Component Rules

- **Max Lines per Component**: Limit components to **200 lines** of code (excluding comments). If a component exceeds this, refactor it into smaller, reusable components or extract logic into hooks/utils.
- **Single Responsibility**: Each component should have one primary responsibility (e.g., rendering a UI element, handling form logic).
- **Props**:
  - Use explicit prop names that describe their purpose (e.g., `userData` instead of `data`).
  - Use defaultProps for optional props and validate with PropTypes (if not using TypeScript).
- **State Management**:
  - Use React hooks (`useState`, `useEffect`, etc.) for state and side effects.
  - Extract complex logic into custom hooks in `/lib/hooks` (e.g., `useAuth`, `useProducts`).
- **Reusable Components**:
  - Store reusable UI components in `/components/ui` (e.g., shadcn/ui components).
  - Store feature-specific components in `/components/feature/[feature-name]`.
- **Server Components**:
  - Use Next.js Server Components by default in the App Router for better performance.
  - Mark client-side components with `"use client"` directive only when necessary (e.g., for interactivity).
- **Styling**:
  - Use Tailwind CSS with shadcn/ui components for consistency.
  - Avoid inline styles unless absolutely necessary.
  - Group related Tailwind classes logically (e.g., layout, spacing, typography).

## 5. MongoDB and API Rules

- **Database Connection**:
  - Centralize MongoDB connection logic in `/lib/db/mongoose.js`.
  - Use environment variables for MongoDB URI (`MONGODB_URI`).
  - Implement connection caching to avoid multiple connections.
- **Mongoose Models**:
  - Define schemas in `/lib/models` with clear, minimal fields.
  - Use Mongoose middleware for common operations (e.g., timestamps).
  - Validate data at the schema level to ensure consistency.
- **API Routes**:
  - Use Next.js API routes in `/app/api` for server-side logic.
  - Organize routes by resource (e.g., `/api/users`, `/api/products`).
  - Handle errors consistently with JSON responses (e.g., `{ error: "Message" }`).
  - Use HTTP status codes appropriately (e.g., 200, 400, 500).
- **Data Fetching**:
  - Use Server Components for data fetching where possible to reduce client-side JavaScript.
  - Use `fetch` or `axios` for external API calls, wrapped in utility functions in `/lib/utils/api.js`.

## 6. Scalability and Maintenance

- **Modular Design**:
  - Break down features into independent modules (e.g., `/components/feature/user`, `/lib/models/user.js`).
  - Avoid deeply nested folder structures (max 3 levels deep).
- **Code Splitting**:
  - Use dynamic imports (`next/dynamic`) for heavy components to reduce bundle size.
  - Leverage Next.js automatic code splitting for pages.
- **Testing**:
  - Write unit tests for utilities and hooks using Jest.
  - Write integration tests for API routes and database operations.
  - Use Playwright or Cypress for end-to-end tests.
- **Documentation**:
  - Maintain a `README.md` with setup instructions, folder structure, and key commands.
- **Error Handling**:
  - Implement global error boundaries in layouts (`/app/layout.js`).
  - Handle MongoDB connection errors gracefully in `/lib/db/mongoose.js`.
- **Performance**:
  - Use Next.js Image component for optimized image loading.
  - Minimize client-side JavaScript by leveraging Server Components.
  - Use MongoDB indexes for frequently queried fields.

## 7. Team Collaboration Rules

- **Code Reviews**:
  - Require at least one reviewer for all pull requests.
  - Check for adherence to naming conventions, component size, and folder structure.
- **Commit Messages**:
  - Use clear, descriptive commit messages (e.g., `feat: add user profile component`, `fix: handle MongoDB connection error`).
  - Follow Conventional Commits for consistency.
- **Branching**:
  - Use feature branches (`feature/user-auth`, `bugfix/login-error`).
  - Keep `main` branch production-ready.
- **Dependency Management**:
  - Regularly update dependencies to avoid security vulnerabilities.
  - Use `npm` or `yarn` consistently across the team.

## 8. Example Component

Below is an example of a well-structured component adhering to the rules:

```markdown
import { useState } from 'react';
import { UiButton } from '@/components/ui/button';
import { UiInput } from '@/components/ui/input';
import { useAuth } from '@/lib/hooks/use-auth';

export function UserProfile({ userData }) {
  const { updateUser } = useAuth();
  const [name, setName] = useState(userData.name);

  const handleUpdate = async () => {
    try {
      await updateUser({ name });
      alert('Profile updated!');
    } catch (error) {
      alert('Error updating profile');
    }
  };

  return (
    <div className="flex flex-col gap-4 p-4">
      <UiInput
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Enter your name"
        className="w-full"
      />
      <UiButton onClick={handleUpdate} className="w-fit">
        Update Profile
      </UiButton>
    </div>
  );
}
```

## 9. Common Issues and Solutions

- **Component Bloat**: If components exceed 200 lines, refactor into smaller components or move logic to hooks.
- **Folder Disorganization**: Stick to the defined structure and avoid placing components in incorrect folders (e.g., page-specific components outside /app).
- **Naming Inconsistencies**: Enforce kebab-case for files and PascalCase for components via [ESLint rules](https://eslint.org/docs/latest/rules/).
- **Scalability Issues**: Use Server Components, dynamic imports, and MongoDB indexes to improve performance as the project grows.

## 10. Getting Started

### Quick Start (Recommended)

The fastest way to start a project following this ruleset is to use the official starter template:

```bash
npx create-next-shadcn-mongo my-app
cd my-app
npm run dev
```

This command creates a complete Next.js project with:
- ✅ Next.js 15 with App Router
- ✅ 45+ ShadCN UI components pre-installed
- ✅ MongoDB integration with Mongoose
- ✅ Authentication foundation
- ✅ Tailwind CSS configuration
- ✅ ESLint and Prettier setup
- ✅ Folder structure following this ruleset
- ✅ Environment variables template

### Manual Setup (Alternative)

If you prefer to set up manually:

1. Initialize a [Next.js](https://nextjs.org/) project: `npx create-next-app@latest my-app --javascript --eslint`
2. Install dependencies: `npm install mongoose shadcn-ui tailwindcss next-auth`
3. Set up Tailwind and shadcn/ui: Follow [shadcn/ui documentation](https://ui.shadcn.com/) for initialization
4. Configure MongoDB connection in `/lib/db/mongoose.js`
5. Create the folder structure as outlined above
6. Set up ESLint and Prettier for code quality
7. Document the setup in README.md

### After Setup

Regardless of your chosen method:
1. Copy `.env.example` to `.env.local` and configure your environment variables
2. Follow the naming conventions and component rules outlined in this document
3. Maintain the folder structure as your project scales

This ruleset and structure will help your team maintain a clean, scalable, and collaborative Next.js project. Adjust as needed based on project requirements, but maintain consistency across the team.
