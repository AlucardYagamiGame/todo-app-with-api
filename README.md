# Todo App with API

A todo list built with React and TypeScript. Todos are stored on a remote REST API: the app loads, creates, updates and deletes them over HTTP and shows loaders and error messages while requests are in progress.

## Features

- Add a todo (the title is trimmed, empty titles are rejected).
- Delete a todo with the `×` button.
- Toggle a todo's completed status.
- Toggle all todos at once with the `toggleAll` checkbox. It is active only when every todo is completed, and only todos whose status actually changes are sent to the API.
- Rename a todo by double-clicking its title:
  - `Enter` or losing focus saves the change;
  - `Esc` cancels editing;
  - an unchanged title just closes the editor;
  - an empty title deletes the todo.
- Filter todos: All / Active / Completed.
- Show the number of active todos and clear all completed todos.
- A loader overlay on each todo while its request is pending, and a temporary todo while a new one is being created.
- Error notifications that hide automatically after 3 seconds or can be closed manually:
  - `Unable to load todos`
  - `Title should not be empty`
  - `Unable to add a todo`
  - `Unable to delete a todo`
  - `Unable to update a todo`

## Tech stack

- [React 18](https://react.dev/) + [TypeScript](https://www.typescriptlang.org/)
- [Vite](https://vitejs.dev/)
- [Bulma](https://bulma.io/) and SCSS for styling
- [classnames](https://github.com/JedWatson/classnames), [react-transition-group](https://reactcommunity.org/react-transition-group/)
- [Cypress](https://www.cypress.io/) for tests
- ESLint, Prettier and Stylelint for code quality

## API

The app talks to the Mate Academy students API (`https://mate.academy/students-api`), a public REST API that provides a `/todos` resource. The base URL is set in [`src/utils/fetchClient.ts`](src/utils/fetchClient.ts) and the endpoints are wrapped in [`src/api/todos.ts`](src/api/todos.ts).

| Method   | Endpoint            | Purpose                      |
| -------- | ------------------- | ---------------------------- |
| `GET`    | `/todos?userId={id}` | Load the user's todos        |
| `POST`   | `/todos`            | Create a todo                |
| `PATCH`  | `/todos/{id}`       | Update a todo (title/status) |
| `DELETE` | `/todos/{id}`       | Delete a todo                |

A todo looks like this:

```ts
type Todo = {
  id: number;
  userId: number;
  title: string;
  completed: boolean;
};
```

Todos are stored per `userId`, which is set by the `USER_ID` constant in `src/api/todos.ts`. To use your own list, change it to another number.

## Getting started

Requirements: Node.js 18+ and npm.

```bash
npm install
npm start
```

The app runs at [http://localhost:3000](http://localhost:3000).

## Scripts

| Command             | Description                                     |
| ------------------- | ----------------------------------------------- |
| `npm start`         | Start the dev server on port 3000               |
| `npm run build`     | Create a production build in `dist/`            |
| `npm run preview`   | Preview the production build                    |
| `npm run lint`      | Run Stylelint, Prettier, ESLint and the type check |
| `npm run typecheck` | Run the TypeScript compiler without emitting    |
| `npm run cypress`   | Open Cypress in interactive mode                |
| `npm test`          | Run Cypress tests headlessly                    |
| `npm run deploy`    | Build and publish `dist/` to GitHub Pages       |

## Project structure

```
src/
├── api/          # API calls (todos.ts)
├── components/   # Header, NewTodo, TodoList, TodoItem, Footer, ErrorNotification
├── styles/       # SCSS styles
├── types/        # Todo, FilterType, ErrorMessage
├── utils/        # fetchClient (HTTP wrapper)
├── App.tsx       # State and API handlers
└── index.tsx
```

## License

MIT. See [LICENSE](LICENSE).
