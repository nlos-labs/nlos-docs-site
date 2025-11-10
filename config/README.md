# Environment Configuration Guide

This document describes the environment variables used in this repository.

## Core Configuration

### APP_ENV
- **Type:** `string`
- **Values:** `development`, `staging`, `production`
- **Description:** Application environment mode
- **Required:** Yes

### LOG_LEVEL
- **Type:** `string`
- **Values:** `debug`, `info`, `warn`, `error`
- **Description:** Logging verbosity level
- **Required:** Yes
- **Default:** `info`

## Supabase Configuration

### SUPABASE_URL
- **Type:** `string` (URL)
- **Description:** Your Supabase project URL
- **Required:** Yes
- **Example:** `https://your-project.supabase.co`

### SUPABASE_ANON_KEY
- **Type:** `string`
- **Description:** Supabase anonymous (public) key for client-side operations
- **Required:** Yes
- **Security:** Safe to expose in client-side code

### SUPABASE_SERVICE_ROLE
- **Type:** `string`
- **Description:** Supabase service role key for server-side operations
- **Required:** Backend services only
- **Security:** ⚠️ NEVER expose in client-side code - bypasses Row Level Security

## Database Configuration

### POSTGRES_URL
- **Type:** `string` (URL)
- **Description:** PostgreSQL database connection string
- **Required:** Backend services only
- **Format:** `postgresql://user:password@host:port/database`
- **Example:** `postgresql://nlos:password@localhost:5432/nlos_db`

## Caching & Queue Configuration

### REDIS_URL
- **Type:** `string` (URL)
- **Description:** Redis connection string for caching
- **Required:** Backend services only
- **Format:** `redis://[username:password@]host:port[/database]`
- **Example:** `redis://localhost:6379`

### QUEUE_URL
- **Type:** `string` (URL)
- **Description:** Message queue connection string (typically Redis)
- **Required:** Backend services with async processing
- **Example:** `redis://localhost:6379`

## AI Services

### OPENAI_API_KEY
- **Type:** `string`
- **Description:** OpenAI API key for AI/ML features
- **Required:** Services using AI features
- **Format:** `sk-...`
- **Security:** ⚠️ Keep secret - never commit to version control

## Vector Database

### QDRANT_URL
- **Type:** `string` (URL)
- **Description:** Qdrant vector database endpoint
- **Required:** Services using vector search
- **Example:** `http://localhost:6333`

## Object Storage (S3-compatible)

### S3_ENDPOINT
- **Type:** `string` (URL)
- **Description:** S3-compatible storage endpoint
- **Required:** Services handling file uploads
- **Example:** `http://localhost:9000` (MinIO), `https://s3.amazonaws.com` (AWS)

### S3_ACCESS_KEY
- **Type:** `string`
- **Description:** S3 access key ID
- **Required:** Services handling file uploads

### S3_SECRET_KEY
- **Type:** `string`
- **Description:** S3 secret access key
- **Required:** Services handling file uploads
- **Security:** ⚠️ Keep secret

### S3_BUCKET
- **Type:** `string`
- **Description:** S3 bucket name for file storage
- **Required:** Services handling file uploads
- **Example:** `nlos-storage`

### S3_REGION
- **Type:** `string`
- **Description:** AWS region for S3 bucket
- **Required:** AWS S3 only
- **Default:** `us-east-1`

## Frontend-Specific Variables

For frontend applications, use `NEXT_PUBLIC_` prefix for variables that need to be exposed to the browser:

### NEXT_PUBLIC_APP_ENV
- Same as `APP_ENV` but accessible in browser

### NEXT_PUBLIC_SUPABASE_URL
- Same as `SUPABASE_URL` but accessible in browser

### NEXT_PUBLIC_API_URL
- **Type:** `string` (URL)
- **Description:** Backend API base URL
- **Example:** `http://localhost:3000/api`

## Development Setup

1. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Fill in your actual values (never commit `.env` file)

3. For local development, you can use the default values provided

4. For production, ensure all required variables are set with secure values

## Security Best Practices

- ✅ DO commit `.env.example` with placeholder values
- ❌ NEVER commit `.env` with actual values
- ❌ NEVER commit API keys, passwords, or secrets
- ✅ DO use different credentials for each environment
- ✅ DO rotate credentials regularly
- ✅ DO use secret management services in production

## Troubleshooting

### Missing Environment Variables
If you see errors about missing environment variables:
1. Check that `.env` file exists
2. Verify all required variables are set
3. Restart your development server

### Invalid Values
If services fail to connect:
1. Verify URLs are correctly formatted
2. Check that services are running (database, Redis, etc.)
3. Verify credentials are correct
