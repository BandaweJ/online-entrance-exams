# Online Entrance Exams - Deployment Guide

This guide will walk you through deploying the Online Entrance Exams application to Render.com.

## Prerequisites

- GitHub account
- Render.com account
- PostgreSQL database (can be created through Render)

## Step 1: Create GitHub Repositories

### Backend Repository
1. Go to GitHub and create a new repository named `online-entrance-exams-backend`
2. Upload the contents of `/online-entrance-exams-backend/` folder
3. Commit and push the code

### Frontend Repository
1. Create another repository named `online-entrance-exams-frontend`
2. Upload the contents of `/online-entrance-exams-frontend/` folder
3. Commit and push the code

## Step 2: Set Up PostgreSQL Database on Render

1. Log in to [Render.com](https://render.com)
2. Click "New +" → "PostgreSQL"
3. Configure the database:
   - **Name**: `entrance-exams-db`
   - **Database**: `entrance_exams`
   - **User**: `entrance_exams_user`
   - **Region**: Choose closest to your users
4. Click "Create Database"
5. Note down the connection details (you'll need these for the backend)

## Step 3: Deploy Backend API

1. In Render dashboard, click "New +" → "Web Service"
2. Connect your GitHub account and select `online-entrance-exams-backend`
3. Configure the service:
   - **Name**: `entrance-exams-api`
   - **Environment**: `Node`
   - **Build Command**: `npm run render:build`
   - **Start Command**: `npm run render:start`
   - **Node Version**: `18`

### Backend Environment Variables
Add these environment variables in the Render dashboard:

```
NODE_ENV=production
PORT=3000
DB_HOST=<your-db-host-from-step-2>
DB_PORT=5432
DB_USERNAME=<your-db-username>
DB_PASSWORD=<your-db-password>
DB_NAME=entrance_exams
JWT_SECRET=<generate-a-secure-random-string>
JWT_EXPIRES_IN=24h
CORS_ORIGIN=https://your-frontend-app-name.onrender.com
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password
TWILIO_ACCOUNT_SID=your-twilio-account-sid
TWILIO_AUTH_TOKEN=your-twilio-auth-token
TWILIO_FROM_NUMBER=your-twilio-phone-number
```

4. Click "Create Web Service"
5. Wait for the deployment to complete
6. Note the backend URL (e.g., `https://entrance-exams-api.onrender.com`)

## Step 4: Deploy Frontend

1. In Render dashboard, click "New +" → "Static Site"
2. Connect your GitHub account and select `online-entrance-exams-frontend`
3. Configure the service:
   - **Name**: `entrance-exams-frontend`
   - **Build Command**: `npm run render:build`
   - **Publish Directory**: `dist/frontend`
   - **Node Version**: `18`

### Frontend Environment Variables
Add these environment variables:

```
NODE_ENV=production
```

4. **Important**: Before deploying, update the frontend environment file:
   - Edit `src/environments/environment.prod.ts`
   - Replace `https://your-backend-app-name.onrender.com/api` with your actual backend URL from Step 3
   - Commit and push the changes

5. Click "Create Static Site"
6. Wait for the deployment to complete
7. Note the frontend URL (e.g., `https://entrance-exams-frontend.onrender.com`)

## Step 5: Update CORS Configuration

1. Go back to your backend service in Render
2. Update the `CORS_ORIGIN` environment variable with your frontend URL
3. Redeploy the backend service

## Step 6: Initialize Database

1. Access your backend service logs in Render
2. Run the database migrations:
   ```bash
   npm run migration:run
   ```
3. Seed the database with an admin user:
   ```bash
   npm run seed
   ```

## Step 7: Test the Application

1. Visit your frontend URL
2. Try to register a new admin user or use the seeded admin credentials
3. Test the exam creation and student management features

## Step 8: Configure Custom Domain (Optional)

1. In your frontend service settings, go to "Custom Domains"
2. Add your domain name
3. Follow the DNS configuration instructions
4. Update the backend `CORS_ORIGIN` to include your custom domain

## Environment Variables Reference

### Backend Required Variables
- `NODE_ENV`: `production`
- `PORT`: `3000` (auto-set by Render)
- `DB_HOST`: Your PostgreSQL host
- `DB_PORT`: `5432`
- `DB_USERNAME`: Your database username
- `DB_PASSWORD`: Your database password
- `DB_NAME`: `entrance_exams`
- `JWT_SECRET`: A secure random string
- `JWT_EXPIRES_IN`: `24h`
- `CORS_ORIGIN`: Your frontend URL

### Backend Optional Variables
- `SMTP_HOST`: Email server host
- `SMTP_PORT`: Email server port
- `SMTP_USER`: Email username
- `SMTP_PASS`: Email password
- `TWILIO_ACCOUNT_SID`: Twilio account SID
- `TWILIO_AUTH_TOKEN`: Twilio auth token
- `TWILIO_FROM_NUMBER`: Twilio phone number

### Frontend Required Variables
- `NODE_ENV`: `production`

## Troubleshooting

### Common Issues

1. **CORS Errors**: Ensure `CORS_ORIGIN` matches your frontend URL exactly
2. **Database Connection**: Verify all database environment variables are correct
3. **Build Failures**: Check the build logs for missing dependencies
4. **Environment Variables**: Ensure all required variables are set

### Logs and Debugging

- Backend logs: Available in the Render dashboard under your backend service
- Frontend logs: Available in the Render dashboard under your frontend service
- Database logs: Available in the Render dashboard under your database service

## Security Considerations

1. **JWT Secret**: Use a strong, random JWT secret
2. **Database Password**: Use a strong database password
3. **CORS**: Only allow your frontend domain
4. **Environment Variables**: Never commit sensitive data to your repository

## Monitoring and Maintenance

1. **Health Checks**: Render automatically monitors your services
2. **Scaling**: Adjust instance count based on usage
3. **Backups**: Render provides automatic database backups
4. **Updates**: Regularly update dependencies and redeploy

## Cost Optimization

1. **Free Tier**: Both services can run on Render's free tier initially
2. **Database**: PostgreSQL free tier includes 1GB storage
3. **Scaling**: Only scale up when needed

## Support

- Render Documentation: https://render.com/docs
- GitHub Issues: Create issues in your repository for bugs
- Community: Render Community Forum

---

## Quick Reference URLs

After deployment, you'll have:
- **Frontend**: `https://entrance-exams-frontend.onrender.com`
- **Backend API**: `https://entrance-exams-api.onrender.com`
- **Database**: Managed by Render

Remember to update the frontend environment file with the correct backend URL before deploying!
