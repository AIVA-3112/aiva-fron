# AIVA Chat Application - Railway Deployment

This document provides instructions for deploying the AIVA Chat Application frontend to Railway.app.

## Overview

This is a standalone frontend application built with React, Vite, and TypeScript that communicates with backend services via REST APIs. The application can be deployed to Railway using their Nixpacks build system.

## Deployment to Railway

### 1. Connect to Railway

1. Sign up or log in to [Railway.app](https://railway.app/)
2. Create a new project
3. Connect your GitHub repository or deploy directly from the CLI

### 2. Environment Variables

Set the following environment variables in your Railway project dashboard:

```env
# API Configuration
VITE_API_URL=https://web-production-50913.up.railway.app/api
VITE_APP_URL=https://your-app-name.up.railway.app

# Authentication settings (if using Microsoft Entra ID)
VITE_MICROSOFT_CLIENT_ID=your-client-id
VITE_MICROSOFT_TENANT_ID=your-tenant-id

# Other OAuth providers (optional)
VITE_GOOGLE_CLIENT_ID=your-google-client-id
VITE_YAHOO_CLIENT_ID=your-yahoo-client-id

# Node.js Configuration
PORT=8080
NODE_ENV=production
```

### 3. Deployment Configuration

The deployment uses the following configuration files:

1. **[railway.json](file:///c%3A/Users/sudhe/Downloads/web-main/web-main/railway.json)** - Railway deployment configuration
2. **[nixpacks.toml](file:///c%3A/Users/sudhe/Downloads/web-main/web-main/nixpacks.toml)** - Nixpacks build configuration

### 4. Build Process

Railway will automatically:
1. Detect the Node.js project
2. Install dependencies using `npm ci`
3. Build the application using `npm run build`
4. Start the application using `npm run preview`

### 5. Custom Domain (Optional)

To use a custom domain:
1. Go to your Railway project settings
2. Navigate to the "Domains" section
3. Add your custom domain
4. Configure DNS records as instructed

## Environment Variables Details

### Required Variables

| Variable | Description | Example Value |
|----------|-------------|---------------|
| `VITE_API_URL` | Backend API endpoint | `https://web-production-50913.up.railway.app/api` |
| `VITE_APP_URL` | Your frontend URL | `https://your-app-name.up.railway.app` |
| `PORT` | Port for the application to listen on | `8080` |
| `NODE_ENV` | Node environment | `production` |

### Optional Authentication Variables

If you're using OAuth authentication providers:

| Variable | Description | Example Value |
|----------|-------------|---------------|
| `VITE_MICROSOFT_CLIENT_ID` | Microsoft OAuth client ID | `your-client-id` |
| `VITE_MICROSOFT_TENANT_ID` | Microsoft tenant ID | `your-tenant-id` |
| `VITE_GOOGLE_CLIENT_ID` | Google OAuth client ID | `your-google-client-id` |
| `VITE_YAHOO_CLIENT_ID` | Yahoo OAuth client ID | `your-yahoo-client-id` |

## Troubleshooting

### Common Issues

1. **Application not starting**: Check that all required environment variables are set
2. **Blank page**: Verify the build completed successfully by checking Railway logs
3. **API connection errors**: Ensure `VITE_API_URL` is correctly set to your backend API
4. **Authentication issues**: Verify OAuth configuration settings

### Checking Logs

To check deployment logs:
1. Go to your Railway project dashboard
2. Click on your service
3. View the "Logs" tab to see real-time output

### Build Issues

If you encounter build errors:

1. **Clean install dependencies**:
   ```bash
   rm -rf node_modules package-lock.json
   npm install
   ```

2. **Check Node.js version compatibility**:
   Ensure you're using Node.js 18.x or later

## Scaling Considerations

Railway automatically handles scaling for you. For high-traffic deployments:

1. **Upgrade your Railway plan** for more resources
2. **Enable autoscaling** in Railway settings
3. **Use Railway's caching features** for improved performance

## Security Best Practices

1. **Always use HTTPS** - Railway provides this automatically
2. **Store secrets securely** using Railway's environment variables
3. **Regularly update dependencies** to address security vulnerabilities
4. **Implement proper authentication and authorization** in your backend services