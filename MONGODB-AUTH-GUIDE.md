# MongoDB Authentication Guide
**Date:** 2026-04-30

---

## Overview

This guide shows how to enable MongoDB authentication for all services.

---

## Step 1: Create MongoDB User (MongoDB Atlas Console)

1. Go to MongoDB Atlas → Security → Database Access
2. Click "Add New Database User"
3. Select "Password" authentication
4. Create user with readWrite role
5. Copy the password

## Step 2: Update Connection Strings

### Current Format:
```
mongodb://host:27017/rez-app
```

### New Format:
```
mongodb://admin:PASSWORD@host:27017/rez-app?authSource=admin
```

## Step 3: Update Environment Variables

### rez-order-service/.env
```env
MONGODB_URI=mongodb://admin:YOUR_PASSWORD@your-cluster.mongodb.net/rez-app?authSource=admin&replicaSet=your-replica-set&w=majority
```

### rez-payment-service/.env
```env
MONGODB_URI=mongodb://admin:YOUR_PASSWORD@your-cluster.mongodb.net/rez-app?authSource=admin
```

### rez-wallet-service/.env
```env
MONGODB_URI=mongodb://admin:YOUR_PASSWORD@your-cluster.mongodb.net/rez-app?authSource=admin
```

### rez-auth-service/.env
```env
MONGODB_URI=mongodb://admin:YOUR_PASSWORD@your-cluster.mongodb.net/rez-app?authSource=admin
```

### rez-merchant-service/.env
```env
MONGODB_URI=mongodb://admin:YOUR_PASSWORD@your-cluster.mongodb.net/rez-app?authSource=admin
```

---

## Step 4: Update render.yaml Files

Add to each service's render.yaml:
```yaml
envVars:
  - key: MONGODB_URI
    value: mongodb://admin:YOUR_PASSWORD@your-cluster.mongodb.net/rez-app?authSource=admin
```

---

## Verification

```bash
# Test connection
mongosh "mongodb://admin:PASSWORD@your-cluster.mongodb.net/rez-app?authSource=admin" --eval "db.runCommand({ ping: 1 })"
```

Expected output:
```json
{ ok: 1 }
```

---

## Rollback

If authentication fails, temporarily set:
```env
MONGODB_URI=mongodb://your-cluster.mongodb.net/rez-app
```

Then debug and re-enable auth.
