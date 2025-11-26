# Environment Variables for Deployment

## 🔴 REQUIRED Environment Variables

### Backend (Node.js/Express)

These are **absolutely essential** for your application to run:

```env
# MongoDB Database Connection
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/Ecommerce-Products
# OR for MongoDB Atlas:
MONGO_URI=mongodb+srv://your-username:your-password@cluster0.xxxxx.mongodb.net/Ecommerce-Products?retryWrites=true&w=majority

# JWT Authentication Secret
JWT_SECRET=your_random_secret_key_here_minimum_32_characters
```

**How to get these:**
- **MONGO_URI**: 
  - Create a free MongoDB Atlas account at https://www.mongodb.com/cloud/atlas
  - Create a cluster (free tier M0)
  - Click "Connect" → "Connect your application"
  - Copy the connection string and replace `<password>` with your database password
- **JWT_SECRET**: Generate a random string (use `openssl rand -base64 32` or any secure random string generator)

---

## 🟡 OPTIONAL but Recommended

### For Product Recommendations (Pinecone)

If you want AI-powered product recommendations to work:

```env
# Pinecone Vector Database (Primary recommendation engine)
PINECONE_API_KEY=your_pinecone_api_key
PINECONE_HOST=https://your-index.svc.us-east-1.pinecone.io
PINECONE_INDEX=ecommerce-products
PINECONE_NAMESPACE=ecommerce-products
GOOGLE_AI_API_KEY=your_google_ai_api_key

# Optional Pinecone settings
PINECONE_TIMEOUT_MS=20000
PINECONE_PURGE_ON_SYNC=true
```

**How to get these:**
- **Pinecone**: Create free account at https://www.pinecone.io
  - Create a serverless index (768 dimensions, cosine metric)
  - Copy your API key and host URL
- **Google AI**: Get API key from https://makersuite.google.com/app/apikey

**Note**: Without Pinecone, recommendations will fall back to basic heuristics (category/brand matching).

### For Weaviate (Alternative Vector Database)

```env
WEAVIATE_HOST=https://your-instance.weaviate.network
WEAVIATE_API_KEY=your_weaviate_api_key
RECOMMENDATION_PREFER_WEAVIATE=false
```

**Note**: Weaviate is optional. Only add if you want to use it as an alternative to Pinecone.

---

## 🟢 Optional Configuration

```env
# Server Port (defaults to 8000 if not set)
PORT=5000

# Database Seeding (prevents auto-seeding on startup)
SKIP_SEED_ON_START=true

# Force re-seed database (clears existing products)
FORCE_SEED_ON_START=false
```

---

## 📋 Quick Setup Checklist for Deployment

### Minimum Setup (Basic E-commerce without AI recommendations):
✅ `MONGO_URI`  
✅ `JWT_SECRET`

### Full Setup (With AI recommendations):
✅ `MONGO_URI`  
✅ `JWT_SECRET`  
✅ `PINECONE_API_KEY`  
✅ `PINECONE_HOST`  
✅ `GOOGLE_AI_API_KEY`  
✅ `PINECONE_INDEX` (optional, defaults to 'ecommerce-products')

---

## 🌐 Platform-Specific Instructions

### Vercel (Frontend + Backend)
1. Go to your project settings
2. Navigate to "Environment Variables"
3. Add all required variables listed above
4. **Important**: Add variables for both "Production" and "Preview" environments
5. Make sure variable names match exactly (case-sensitive)

### Render (Backend only)
1. Go to your service dashboard
2. Click "Environment" tab
3. Add each variable with "Add Environment Variable"
4. Add `MONGO_URI` and `JWT_SECRET` at minimum

### Railway / Heroku / Other Platforms
1. Find "Environment Variables" or "Config Vars" section
2. Add each variable manually or upload `.env` file
3. **Never commit `.env` file** - it's in `.gitignore` for your protection

---

## 🔒 Security Best Practices

1. **Never commit `.env` files** - They're already in `.gitignore`
2. **Generate strong JWT_SECRET** - Use at least 32 random characters
3. **Use MongoDB connection string with username/password** - Don't expose in code
4. **Rotate API keys periodically** - Especially if they're exposed in logs

---

## ⚠️ Common Issues

### Issue: "MongoDB connection error"
**Solution**: Check your `MONGO_URI` is correct and MongoDB Atlas IP whitelist includes `0.0.0.0/0` (or your server's IP)

### Issue: "Pinecone sync error"
**Solution**: App will continue running, but recommendations will use fallback heuristics. Check your Pinecone API key and host URL.

### Issue: "JWT_SECRET must be set"
**Solution**: Add `JWT_SECRET` to your environment variables. This is required for user authentication.

---

## 🧪 Testing Your Setup

After deployment, test these endpoints:
- `GET /api/products` - Should return product list
- `GET /api-docs` - Should show Swagger documentation
- `POST /api/auth/register` - Should create new user (if JWT_SECRET is set)


