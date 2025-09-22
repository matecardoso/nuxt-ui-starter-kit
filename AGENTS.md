# AI Agents Guide

## Project Context

When working with this Laravel + Vue starter kit, please read the `llms.txt` file first to understand the project structure, technology stack, and development practices.

## Important Notes for AI Agents

1. **Read the Context**: Always start by reading `llms.txt` to understand the project's architecture and conventions.

2. **Project Type**: This is a Laravel application with Vue.js frontend using Inertia.js, not a Nuxt.js application (despite the repository name).

3. **Technology Stack**:
   - Backend: Laravel with PHP
   - Frontend: Vue 3 + TypeScript
   - Build Tool: Vite
   - CSS Framework: Tailwind CSS 4.x
   - UI Components: shadcn-vue
   - SPA Framework: Inertia.js

4. **Code Structure**:
   - Vue components are in `resources/js/components/`
   - Pages are in `resources/js/pages/`
   - Layouts are in `resources/js/layouts/`
   - Laravel controllers and models are in `app/`

5. **Development Workflow**:
   - Install dependencies: `npm install` and `composer install`
   - Development: `npm run dev` and `php artisan serve`
   - Linting: `npm run lint`
   - Building: `npm run build`

6. **Best Practices**:
   - Follow Vue 3 Composition API patterns
   - Use TypeScript for type safety
   - Follow Tailwind CSS utility-first approach
   - Maintain consistency with existing component structure
   - Use shadcn-vue component patterns

## File Conventions

- Vue components use PascalCase naming
- TypeScript files use camelCase
- CSS classes follow Tailwind conventions
- Laravel follows PSR-4 autoloading standards

## Testing

- PHP: PHPUnit for backend testing
- JavaScript: No frontend testing framework currently configured

Always refer to the existing codebase for patterns and conventions before making changes.