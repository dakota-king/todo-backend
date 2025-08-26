# Todo Backend API

A RESTful API for a Todo List application built with Express.js, TypeScript, Prisma, and MySQL.

## Features

- 🚀 RESTful API with full CRUD operations
- 🛡️ TypeScript for type safety
- 🗄️ MySQL database with Prisma ORM
- 🔒 Input validation and error handling
- 🌐 CORS enabled for frontend integration
- ⚡ Fast and lightweight Express.js server

## Tech Stack

- **Express.js** - Web framework for Node.js
- **TypeScript** - Type safety and better development experience
- **Prisma** - Modern database toolkit and ORM
- **MySQL** - Relational database
- **CORS** - Cross-origin resource sharing
- **dotenv** - Environment variable management

## Getting Started

### Prerequisites

- Node.js 18+
- npm or yarn
- MySQL database (local or cloud)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd todo-backend
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
```

4. Update the `.env` file with your database credentials:
```env
DATABASE_URL="mysql://username:password@localhost:3306/todo_db"
PORT=5000
```

5. Set up the database:
```bash
# Generate Prisma client
npm run db:generate

# Push the schema to your database
npm run db:push

# Or run migrations (alternative to db:push)
npm run db:migrate
```

6. Start the development server:
```bash
npm run dev
```

The API will be available at `http://localhost:5000`

## Available Scripts

- `npm run dev` - Start development server with hot reload
- `npm run build` - Build TypeScript to JavaScript
- `npm run start` - Start production server
- `npm run db:generate` - Generate Prisma client
- `npm run db:push` - Push schema changes to database
- `npm run db:migrate` - Run database migrations

## API Endpoints

### Health Check
- `GET /api/health` - Check if API is running

### Tasks
- `GET /api/tasks` - Get all tasks
- `POST /api/tasks` - Create a new task
- `PUT /api/tasks/:id` - Update a task
- `DELETE /api/tasks/:id` - Delete a task

## API Documentation

### Get All Tasks
```http
GET /api/tasks
```

**Response:**
```json
[
  {
    "id": 1,
    "title": "Complete project",
    "color": "blue",
    "completed": false,
    "createdAt": "2024-01-01T00:00:00.000Z",
    "updatedAt": "2024-01-01T00:00:00.000Z"
  }
]
```

### Create Task
```http
POST /api/tasks
Content-Type: application/json

{
  "title": "New task",
  "color": "red"
}
```

**Response:**
```json
{
  "id": 2,
  "title": "New task",
  "color": "red",
  "completed": false,
  "createdAt": "2024-01-01T00:00:00.000Z",
  "updatedAt": "2024-01-01T00:00:00.000Z"
}
```

### Update Task
```http
PUT /api/tasks/1
Content-Type: application/json

{
  "title": "Updated task",
  "color": "green",
  "completed": true
}
```

### Delete Task
```http
DELETE /api/tasks/1
```

**Response:** `204 No Content`

## Database Schema

### Task Model
```prisma
model Task {
  id        Int      @id @default(autoincrement())
  title     String
  color     String   @default("blue")
  completed Boolean  @default(false)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  @@map("tasks")
}
```

## Project Structure

```
src/
└── index.ts            # Main application file with routes
prisma/
├── schema.prisma       # Database schema
└── migrations/         # Database migrations (if using migrations)
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `DATABASE_URL` | MySQL connection string | Required |
| `PORT` | Server port | 5000 |

## Error Handling

The API includes comprehensive error handling:

- **400 Bad Request** - Invalid input data
- **404 Not Found** - Task not found
- **500 Internal Server Error** - Server errors

## CORS Configuration

CORS is enabled to allow requests from the frontend application. In production, configure CORS to only allow requests from your frontend domain.

## Database Setup

### Using MySQL locally:

1. Install MySQL on your system
2. Create a database:
```sql
CREATE DATABASE todo_db;
```
3. Update the `DATABASE_URL` in your `.env` file
4. Run `npm run db:push` to create tables

### Using Cloud Database:

You can use cloud providers like:
- PlanetScale
- AWS RDS
- Google Cloud SQL
- Azure Database for MySQL

Just update the `DATABASE_URL` with your cloud database connection string.

## Deployment

### Using PM2 (Production):
```bash
npm install -g pm2
npm run build
pm2 start dist/index.js --name "todo-api"
```

### Using Docker:
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 5000
CMD ["npm", "start"]
```

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-feature`
3. Commit your changes: `git commit -am 'Add new feature'`
4. Push to the branch: `git push origin feature/new-feature`
5. Submit a pull request

## License

This project is licensed under the MIT License.
