# 🚀 ChatTTK - GOD++ EDITION (V14 - ULTRA UPGRADED)

## 👤 Giới Thiệu

ChatTTK là một ứng dụng chat enterprise cấp độ GOD++ với khả năng scale vô hạn, được xây dựng trên nền tảng Firebase Serverless và Google Cloud. Ứng dụng tích hợp đầy đủ các tính năng hiện đại: real-time messaging, video calls, livestream, stories, AI assistant, và hệ thống quản trị mạnh mẽ. Tất cả file upload được xử lý bởi **UploadThing** - dịch vụ upload file hiện đại, miễn phí 5GB/tháng và tích hợp native với Vercel.

### ✨ Tính Năng Chính

- **💬 Real-time Messaging**: Chat 1-1 và nhóm với khả năng xử lý 15,000+ tin nhắn mượt mà
- **📹 Video Calls & Livestream**: Video call nhóm, livestream với chat overlay
- **📸 Stories 24h**: Tạo và xem stories tự động xóa sau 24 giờ
- **🤖 AI Integration**: AI assistant, smart replies, sentiment analysis
- **👥 Social Features**: Friend system, groups, mentions, hashtags
- **🛒 E-Commerce**: In-app shop, payment integration, subscription tiers
- **🛡️ Security**: End-to-end encryption, 2FA, rate limiting, DDoS protection
- **👑 Admin Panel**: Dashboard analytics, user management, content moderation
- **📁 File Upload**: Upload hình ảnh, video, file với UploadThing (FREE 5GB/tháng)

### 🛠 Tech Stack

**Frontend:**
- React 18 + TypeScript (Strict Mode)
- Vite + TailwindCSS v4 + DaisyUI
- Zustand (State Management) + TanStack Query v5
- TanStack Virtual (Virtualization)
- WebRTC (Video Calls), HLS.js (Livestream)
- PWA Support (Workbox)
- **UploadThing React SDK** (`@uploadthing/react`)

**Backend:**
- **Vercel Serverless Functions** (Node.js 20) - Thay thế Firebase Functions
- Firestore (Database) + Realtime Database (Presence)
- **UploadThing Server** (`uploadthing/server`) - Thay thế Firebase Storage
- Firebase Auth (Email, Google, GitHub, Discord, Apple)
- **Vercel Cron Jobs** - Scheduled tasks
- Vertex AI, OpenAI, Claude, Gemini (AI)
- Cloud Video Intelligence API
- SendGrid (Email), Twilio (SMS)

**File Storage:**
- **UploadThing** - File upload service (FREE 5GB/tháng)
  - Native Vercel integration
  - Type-safe uploads
  - Built-in file validation
  - CDN delivery
  - Automatic optimization

**Deployment:**
- **Vercel** - Full-stack deployment (Frontend + Backend)
  - Automatic HTTPS & CDN
  - Edge Network worldwide
  - Serverless Functions auto-scaling
  - Built-in CI/CD với GitHub
  - Real-time logs & monitoring

---

## 📋 Prerequisites & Setup

### Yêu Cầu Hệ Thống

- **Node.js**: >= 20.0.0
- **npm**: >= 10.0.0
- **Firebase CLI**: >= 12.0.0
- **Git**: Latest version
- **UploadThing Account**: [Tạo tài khoản miễn phí](https://uploadthing.com)

### Cài Đặt Firebase CLI

```bash
npm install -g firebase-tools
firebase login
```

### Clone Repository

```bash
git clone <repository-url>
cd chatttkrealtimev5
```

### Cài Đặt Dependencies

```bash
# Install root dependencies
npm install

# Install frontend dependencies
cd frontend
npm install

# Install functions dependencies
cd ../functions
npm install
```

---

## 🔥 Thiết Lập Firebase Chi Tiết

### Bước 1: Tạo Firebase Project

1. Truy cập [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project"
3. Nhập tên project (ví dụ: `chatttk-production`)
4. Chọn Google Analytics (tùy chọn)
5. Click "Create project"

### Bước 2: Cấu Hình Authentication

1. Vào **Authentication** > **Sign-in method**
2. Enable các providers:
   - **Email/Password**: Enable
   - **Google**: Enable (cần OAuth client ID)
   - **GitHub**: Enable (cần OAuth app)
   - **Discord**: Enable (cần OAuth app)
   - **Apple**: Enable (cần Apple Developer account)

#### Cấu hình Google Sign-In:
- Vào [Google Cloud Console](https://console.cloud.google.com/)
- Tạo OAuth 2.0 Client ID
- Thêm authorized redirect URIs: `https://your-project.firebaseapp.com/__/auth/handler`
- Copy Client ID và Client Secret vào Firebase

#### Cấu hình GitHub Sign-In:
- Vào GitHub Settings > Developer settings > OAuth Apps
- Tạo OAuth App mới
- Authorization callback URL: `https://your-project.firebaseapp.com/__/auth/handler`
- Copy Client ID và Client Secret vào Firebase

### Bước 3: Enable Firestore Database

1. Vào **Firestore Database** > **Create database**
2. Chọn **Start in production mode** (sẽ cấu hình rules sau)
3. Chọn location: **asia-southeast1** (Singapore)
4. Click "Enable"

### Bước 4: Enable Realtime Database

1. Vào **Realtime Database** > **Create database**
2. Chọn location: **asia-southeast1**
3. Click "Enable"

**⚠️ Lưu ý: Firebase Storage KHÔNG cần enable vì chúng ta sử dụng UploadThing**

### Bước 5: Setup Firebase Emulator (Local Development)

1. Cài đặt emulator suite:
```bash
firebase init emulators
```

2. Chọn các emulators:
   - Authentication
   - Firestore
   - Functions
   - Realtime Database
   - **KHÔNG chọn Storage** (vì dùng UploadThing)

3. Chạy emulators:
```bash
npm run emulators
```

Emulators sẽ chạy tại:
- Auth: http://localhost:9099
- Firestore: http://localhost:8080
- Functions: http://localhost:5001
- UI: http://localhost:4000

### Bước 6: Tải Service Account Key

1. Vào **Project Settings** > **Service accounts**
2. Click "Generate new private key"
3. Lưu file JSON vào `functions/service-account-key.json` (không commit file này!)
4. Thêm vào `.gitignore`:
```
functions/service-account-key.json
```

---

## 📤 Thiết Lập UploadThing

### Bước 1: Tạo UploadThing Account

1. Truy cập [UploadThing Dashboard](https://uploadthing.com)
2. Đăng ký tài khoản miễn phí (FREE 5GB/tháng)
3. Tạo app mới hoặc chọn app có sẵn

### Bước 2: Lấy API Keys

1. Vào **API Keys** trong UploadThing Dashboard
2. Copy các keys:
   - **UPLOADTHING_SECRET**: Secret key cho server
   - **UPLOADTHING_APP_ID**: App ID (tự động tạo)

### Bước 3: Cài Đặt UploadThing Packages

**Frontend:**
```bash
cd frontend
npm install @uploadthing/react uploadthing
```

**Functions (Backend):**
```bash
cd functions
npm install uploadthing @uploadthing/server
```

### Bước 4: Tạo UploadThing Server Handler

**Option 1: Sử dụng Vercel Serverless Functions (Recommended cho Production)**

Tạo file `api/uploadthing/core.ts` (trong root project, để deploy lên Vercel):

```typescript
import { createUploadthing, type FileRouter } from "uploadthing/next";
import { auth } from "firebase-admin";
import { initializeApp, cert, getApps } from "firebase-admin/app";

// Initialize Firebase Admin
if (!getApps().length) {
  initializeApp({
    credential: cert(JSON.parse(process.env.FIREBASE_SERVICE_ACCOUNT || "{}")),
  });
}

const f = createUploadthing();

// Authentication middleware
const middleware = async (req: Request) => {
  // Get Firebase Auth token from Authorization header
  const authHeader = req.headers.get("authorization");
  if (!authHeader?.startsWith("Bearer ")) {
    throw new Error("Unauthorized");
  }

  const token = authHeader.split("Bearer ")[1];
  
  try {
    // Verify Firebase token
    const decodedToken = await auth().verifyIdToken(token);
    return { userId: decodedToken.uid };
  } catch (error) {
    throw new Error("Invalid token");
  }
};

export const ourFileRouter = {
  // Avatar uploader
  avatarUploader: f({ image: { maxFileSize: "5MB", maxFileCount: 1 } })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      console.log("Avatar uploaded", file.url);
      return { uploadedBy: metadata.userId };
    }),

  // Message attachment uploader (images, videos, files)
  messageUploader: f({
    image: { maxFileSize: "10MB", maxFileCount: 10 },
    video: { maxFileSize: "100MB", maxFileCount: 5 },
    pdf: { maxFileSize: "50MB", maxFileCount: 5 },
    "application/*": { maxFileSize: "100MB", maxFileCount: 5 },
  })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      console.log("Message attachment uploaded", file.url);
      return { uploadedBy: metadata.userId };
    }),

  // Story uploader (images, videos)
  storyUploader: f({
    image: { maxFileSize: "50MB", maxFileCount: 1 },
    video: { maxFileSize: "100MB", maxFileCount: 1 },
  })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      console.log("Story uploaded", file.url);
      return { uploadedBy: metadata.userId };
    }),

  // Group icon uploader
  groupIconUploader: f({ image: { maxFileSize: "5MB", maxFileCount: 1 } })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      console.log("Group icon uploaded", file.url);
      return { uploadedBy: metadata.userId };
    }),

  // Livestream thumbnail uploader
  livestreamThumbnailUploader: f({
    image: { maxFileSize: "10MB", maxFileCount: 1 },
  })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      console.log("Livestream thumbnail uploaded", file.url);
      return { uploadedBy: metadata.userId };
    }),
} satisfies FileRouter;

export type OurFileRouter = typeof ourFileRouter;
```

Tạo file `api/uploadthing/route.ts` (Vercel Serverless Function):

```typescript
import { createRouteHandler } from "uploadthing/next";
import { ourFileRouter } from "./core";

export const { GET, POST } = createRouteHandler({
  router: ourFileRouter,
});
```

**Option 2: Sử dụng Cloud Functions (Firebase Functions)**

Tạo file `functions/src/uploadthing/router.ts`:

```typescript
import { createUploadthing, type FileRouter } from "@uploadthing/server";
import { verifyAuth } from "../middleware/auth";

const f = createUploadthing();

const middleware = async (req: any) => {
  const userId = await verifyAuth(req);
  return { userId };
};

export const ourFileRouter = {
  avatarUploader: f({ image: { maxFileSize: "5MB", maxFileCount: 1 } })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      return { uploadedBy: metadata.userId };
    }),

  messageUploader: f({
    image: { maxFileSize: "10MB", maxFileCount: 10 },
    video: { maxFileSize: "100MB", maxFileCount: 5 },
    pdf: { maxFileSize: "50MB", maxFileCount: 5 },
  })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      return { uploadedBy: metadata.userId };
    }),

  storyUploader: f({
    image: { maxFileSize: "50MB", maxFileCount: 1 },
    video: { maxFileSize: "100MB", maxFileCount: 1 },
  })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      return { uploadedBy: metadata.userId };
    }),

  groupIconUploader: f({ image: { maxFileSize: "5MB", maxFileCount: 1 } })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      return { uploadedBy: metadata.userId };
    }),

  livestreamThumbnailUploader: f({
    image: { maxFileSize: "10MB", maxFileCount: 1 },
  })
    .middleware(middleware)
    .onUploadComplete(async ({ metadata, file }) => {
      return { uploadedBy: metadata.userId };
    }),
} satisfies FileRouter;

export type OurFileRouter = typeof ourFileRouter;
```

Tạo HTTP endpoint trong `functions/src/index.ts`:

```typescript
import { onRequest } from "firebase-functions/v2/https";
import { createUploadthingHandler } from "@uploadthing/server";
import { ourFileRouter } from "./uploadthing/router";

export const uploadthing = onRequest(
  { cors: true, region: "asia-southeast1" },
  createUploadthingHandler({
    router: ourFileRouter,
  })
);
```

### Bước 5: Tạo UploadThing Client Utility

Tạo file `frontend/src/lib/uploadthing.ts`:

```typescript
import {
  generateUploadButton,
  generateUploadDropzone,
  generateUploader,
} from "@uploadthing/react";

import type { OurFileRouter } from "../types/uploadthing";

// Get upload URL from environment
const getUploadUrl = () => {
  if (import.meta.env.PROD) {
    // Production: Use Vercel API route
    return "/api/uploadthing";
  }
  // Development: Use local server or Cloud Functions URL
  return import.meta.env.VITE_UPLOADTHING_URL || "/api/uploadthing";
};

export const UploadButton = generateUploadButton<OurFileRouter>({
  url: getUploadUrl(),
});

export const UploadDropzone = generateUploadDropzone<OurFileRouter>({
  url: getUploadUrl(),
});

export const useUploadThing = generateUploader<OurFileRouter>({
  url: getUploadUrl(),
});
```

Tạo file `frontend/src/types/uploadthing.ts` để export type:

```typescript
// This file will be generated from your server file router
// Or manually type it based on your server router

export type OurFileRouter = {
  avatarUploader: {
    input: Record<string, never>;
    output: { uploadedBy: string };
  };
  messageUploader: {
    input: Record<string, never>;
    output: { uploadedBy: string };
  };
  storyUploader: {
    input: Record<string, never>;
    output: { uploadedBy: string };
  };
  groupIconUploader: {
    input: Record<string, never>;
    output: { uploadedBy: string };
  };
  livestreamThumbnailUploader: {
    input: Record<string, never>;
    output: { uploadedBy: string };
  };
};
```

---

## ⚙️ Environment Configuration

### Frontend Environment Variables

1. Tạo file `.env` trong thư mục `frontend/`:
```bash
cd frontend
cp .env.example .env
```

2. Cập nhật các giá trị trong `.env`:
```env
# Firebase Config
VITE_FIREBASE_API_KEY=your-firebase-api-key
VITE_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your-project-id
VITE_FIREBASE_MESSAGING_SENDER_ID=your-messaging-sender-id
VITE_FIREBASE_APP_ID=your-app-id
VITE_FIREBASE_DATABASE_URL=https://your-project-default-rtdb.firebaseio.com
VITE_FCM_VAPID_KEY=your-fcm-vapid-key

# UploadThing Config (for client-side)
VITE_UPLOADTHING_URL=/api/uploadthing
VITE_UPLOADTHING_APP_ID=your-uploadthing-app-id

# Development
VITE_USE_EMULATORS=true
```

**Lấy Firebase Config:**
- Vào Firebase Console > Project Settings > General
- Scroll xuống "Your apps" > Web app
- Copy các giá trị config

**Lấy FCM VAPID Key:**
- Vào Firebase Console > Project Settings > Cloud Messaging
- Scroll xuống "Web configuration" > Web Push certificates
- Generate key pair nếu chưa có

**Lấy UploadThing App ID:**
- Vào UploadThing Dashboard > API Keys
- Copy App ID

### Functions Environment Variables

1. Tạo file `.env` trong thư mục `functions/`:
```bash
cd functions
cp .env.example .env
```

2. Cập nhật các giá trị:
```env
# AI Services
OPENAI_API_KEY=your-openai-api-key
ANTHROPIC_API_KEY=your-anthropic-api-key
GEMINI_API_KEY=your-gemini-api-key

# Email Service
SENDGRID_API_KEY=your-sendgrid-api-key
SENDGRID_FROM_EMAIL=noreply@chatttk.com

# UploadThing Server
UPLOADTHING_SECRET=your-uploadthing-secret-key
UPLOADTHING_APP_ID=your-uploadthing-app-id

# App URLs
FRONTEND_URL=http://localhost:3000
```

**Lấy API Keys:**
- **OpenAI**: https://platform.openai.com/api-keys
- **Anthropic**: https://console.anthropic.com/
- **Gemini**: https://makersuite.google.com/app/apikey
- **SendGrid**: https://app.sendgrid.com/settings/api_keys
- **UploadThing**: UploadThing Dashboard > API Keys

### Set Environment Variables cho Cloud Functions

```bash
firebase functions:config:set \
  openai.api_key="your-openai-api-key" \
  anthropic.api_key="your-anthropic-api-key" \
  sendgrid.api_key="your-sendgrid-api-key" \
  uploadthing.secret="your-uploadthing-secret-key" \
  uploadthing.app_id="your-uploadthing-app-id" \
  frontend.url="https://your-domain.com"
```

---

## 🚀 Deploy Backend Chi Tiết

### Option 1: Deploy Backend lên Vercel (Recommended)

Backend được deploy cùng frontend lên Vercel. Xem phần **"🌐 Deployment to Vercel (Frontend + Backend)"** ở trên để biết chi tiết.

**Tóm tắt:**
- Tất cả API routes trong folder `api/` tự động được deploy
- Vercel Cron Jobs được config trong `vercel.json`
- Environment variables được set trong Vercel Dashboard

**Deploy commands:**
```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel

# Production deploy
vercel --prod
```

### Option 2: Deploy Backend lên Firebase Functions (Legacy)

Nếu bạn vẫn muốn giữ một số functions trên Firebase (ví dụ: Firestore triggers):

```bash
# Build Functions
cd functions
npm run build

# Deploy Functions
firebase deploy --only functions

# Deploy Firestore Rules
firebase deploy --only firestore:rules

# Deploy Firestore Indexes
firebase deploy --only firestore:indexes
```

### Test Functions Locally

**Vercel Functions:**
```bash
# Install Vercel CLI
npm install -g vercel

# Run locally
vercel dev

# Test API route
curl http://localhost:3000/api/messages/send
```

**Firebase Functions (Legacy):**
```bash
# Chạy emulator
npm run emulators

# Test function
curl http://localhost:5001/your-project/asia-southeast1/users/me
```

---

## 👑 Cấu Hình Admin Tự Động

### Super Admin Email

Hệ thống tự động nhận diện và cấp quyền "GOD MODE" cho email:
- **Email**: `khangnek705@gmail.com`
- **Password mặc định**: `Khang11222013@#`

### Cơ Chế Hoạt Động

1. Khi user đăng ký với email `khangnek705@gmail.com`, trigger `onUserCreate` sẽ:
   - Set Custom Claims: `{ admin: true, godMode: true, role: 'owner', permissions: ['*'] }`
   - Update Firestore user document với các quyền tương ứng
   - Log action vào audit_logs

2. Custom Claims được tự động refresh khi user đăng nhập lại

### Thêm/Xóa Admin

**Thêm Admin (God Mode only):**
```typescript
// Trong Cloud Functions hoặc Admin SDK
await auth.setCustomUserClaims(userId, {
  admin: true,
  godMode: true,
  role: 'owner',
  permissions: ['*'],
});
```

**Xóa Admin:**
```typescript
await auth.setCustomUserClaims(userId, {
  admin: false,
  godMode: false,
  role: 'user',
  permissions: [],
});
```

### Admin Permissions Breakdown

- **GOD MODE** (`godMode: true`):
  - Full quyền sinh sát
  - Access audit logs
  - System configuration
  - Bulk operations

- **ADMIN** (`admin: true`):
  - User management (ban/unban)
  - Content moderation
  - View analytics
  - Manage reports

---

## 💻 Chạy Frontend

### Development Mode

```bash
cd frontend
npm run dev
```

Frontend sẽ chạy tại: http://localhost:3000

### Build Production

```bash
cd frontend
npm run build
```

Output sẽ ở thư mục `frontend/dist/`

### Preview Production Build

```bash
cd frontend
npm run preview
```

---

## 🌐 Deployment to Vercel (Frontend + Backend)

Hệ thống được deploy hoàn toàn trên Vercel, bao gồm:
- **Frontend**: React/Vite app
- **Backend**: Vercel Serverless Functions (thay thế Firebase Functions)
- **File Upload**: UploadThing native integration

---

### Bước 1: Chuẩn Bị Project Structure

**Cấu trúc mới với Vercel:**

```
chatttkrealtimev5/
├── api/                      # Vercel Serverless Functions
│   ├── uploadthing/
│   │   ├── core.ts          # UploadThing file router
│   │   └── route.ts         # UploadThing API handler
│   ├── messages/
│   │   └── send.ts          # POST /api/messages/send
│   ├── groups/
│   │   ├── create.ts        # POST /api/groups/create
│   │   └── [id].ts          # GET/PUT/DELETE /api/groups/[id]
│   ├── calls/
│   │   └── start.ts         # POST /api/calls/start
│   ├── stories/
│   │   └── create.ts        # POST /api/stories/create
│   ├── admin/
│   │   └── actions.ts       # POST /api/admin/actions
│   └── webhooks/
│       ├── stripe.ts        # POST /api/webhooks/stripe
│       └── twilio.ts        # POST /api/webhooks/twilio
├── frontend/                 # React frontend
├── vercel.json              # Vercel configuration
└── cron.json                # Vercel Cron Jobs configuration
```

### Bước 2: Cài Đặt Vercel CLI

```bash
npm install -g vercel
vercel login
```

### Bước 3: Tạo vercel.json

Tạo file `vercel.json` trong root project:

```json
{
  "version": 2,
  "buildCommand": "cd frontend && npm run build",
  "outputDirectory": "frontend/dist",
  "installCommand": "npm install",
  "framework": "vite",
  "rewrites": [
    {
      "source": "/api/(.*)",
      "destination": "/api/$1"
    },
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ],
  "functions": {
    "api/**/*.ts": {
      "memory": 1024,
      "maxDuration": 30
    },
    "api/webhooks/*.ts": {
      "memory": 512,
      "maxDuration": 10
    }
  },
  "crons": [
    {
      "path": "/api/cron/cleanup-stories",
      "schedule": "0 * * * *"
    },
    {
      "path": "/api/cron/generate-analytics",
      "schedule": "0 0 * * *"
    },
    {
      "path": "/api/cron/backup-database",
      "schedule": "0 0 * * 0"
    },
    {
      "path": "/api/cron/send-daily-summary",
      "schedule": "0 9 * * *"
    },
    {
      "path": "/api/cron/cleanup-deleted-users",
      "schedule": "0 2 * * *"
    }
  ],
  "env": {
    "NODE_ENV": "production"
  }
}
```

### Bước 4: Migrate Firebase Functions sang Vercel API Routes

#### 4.1. Callable Functions → API Routes

**Ví dụ: Migrate `sendMessage` function**

**Firebase Functions (Old):**
```typescript
// functions/src/callable/sendMessage.ts
export const sendMessage = onCall(async (request) => {
  // ...
});
```

**Vercel API Route (New):**
```typescript
// api/messages/send.ts
import type { VercelRequest, VercelResponse } from '@vercel/node';
import { verifyAuth } from '../../../lib/middleware/auth';
import { createMessage } from '../../../lib/utils/firestore';

export default async function handler(
  req: VercelRequest,
  res: VercelResponse
) {
  if (req.method !== 'POST') {
    return res.status(405).json({ error: 'Method not allowed' });
  }

  try {
    // Verify authentication
    const userId = await verifyAuth(req);
    
    // Create message
    const messageId = await createMessage({
      conversationId: req.body.conversationId,
      senderId: userId,
      content: req.body.content,
      type: req.body.type,
      fileUrl: req.body.fileUrl,
    });

    return res.status(200).json({
      success: true,
      messageId,
    });
  } catch (error: any) {
    return res.status(500).json({
      error: error.message || 'Internal server error',
    });
  }
}
```

#### 4.2. Scheduled Functions → Vercel Cron Jobs

**Tạo file `api/cron/cleanup-stories.ts`:**

```typescript
// api/cron/cleanup-stories.ts
import type { VercelRequest, VercelResponse } from '@vercel/node';
import { getFirestore } from 'firebase-admin/firestore';

const db = getFirestore();

export default async function handler(
  req: VercelRequest,
  res: VercelResponse
) {
  // Verify cron secret (optional but recommended)
  const authHeader = req.headers.authorization;
  if (authHeader !== `Bearer ${process.env.CRON_SECRET}`) {
    return res.status(401).json({ error: 'Unauthorized' });
  }

  try {
    const now = new Date();
    const twentyFourHoursAgo = new Date(now.getTime() - 24 * 60 * 60 * 1000);

    const storiesSnapshot = await db
      .collection('stories')
      .where('createdAt', '<', twentyFourHoursAgo)
      .limit(500)
      .get();

    const deletePromises = storiesSnapshot.docs.map((doc) => doc.ref.delete());
    await Promise.all(deletePromises);

    return res.status(200).json({
      success: true,
      deleted: storiesSnapshot.size,
    });
  } catch (error: any) {
    console.error('Error in cleanup-stories:', error);
    return res.status(500).json({ error: error.message });
  }
}
```

**Cron Jobs Configuration trong `vercel.json`:**
```json
{
  "crons": [
    {
      "path": "/api/cron/cleanup-stories",
      "schedule": "0 * * * *"
    }
  ]
}
```

#### 4.3. Firestore Triggers → API Routes + Webhooks

**Option 1: Sử dụng Firebase Extensions**

Giữ Firestore triggers trên Firebase và call Vercel API routes:

```typescript
// functions/src/triggers/onMessageSent.ts
import { onDocumentCreated } from 'firebase-functions/v2/firestore';
import axios from 'axios';

export const onMessageSent = onDocumentCreated(
  'conversations/{conversationId}/messages/{messageId}',
  async (event) => {
    // Process locally
    const messageData = event.data?.data();
    
    // Call Vercel API if needed
    await axios.post(`${process.env.VERCEL_API_URL}/api/webhooks/message-sent`, {
      messageData,
    });
  }
);
```

**Option 2: Migrate to Event-driven Architecture**

Sử dụng Firestore triggers + Vercel webhooks:

```typescript
// api/webhooks/firestore-message.ts
import type { VercelRequest, VercelResponse } from '@vercel/node';

export default async function handler(
  req: VercelRequest,
  res: VercelResponse
) {
  // Handle Firestore webhook
  const event = req.body;
  
  if (event.type === 'message.created') {
    // Process message notification
    await sendNotifications(event.data);
  }

  return res.status(200).json({ received: true });
}
```

#### 4.4. Webhooks → API Routes

**Migrate Stripe Webhook:**

```typescript
// api/webhooks/stripe.ts
import type { VercelRequest, VercelResponse } from '@vercel/node';
import Stripe from 'stripe';

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY!, {
  apiVersion: '2023-10-16',
});

export default async function handler(
  req: VercelRequest,
  res: VercelResponse
) {
  const sig = req.headers['stripe-signature'] as string;

  try {
    const event = stripe.webhooks.constructEvent(
      req.body,
      sig,
      process.env.STRIPE_WEBHOOK_SECRET!
    );

    switch (event.type) {
      case 'payment_intent.succeeded':
        await handlePaymentSuccess(event.data.object);
        break;
      // ... other events
    }

    return res.status(200).json({ received: true });
  } catch (error: any) {
    return res.status(400).json({ error: error.message });
  }
}
```

### Bước 5: Setup Shared Utilities

Tạo folder `lib/` trong root để share code giữa API routes:

```
lib/
├── middleware/
│   ├── auth.ts          # Authentication middleware
│   └── rateLimit.ts     # Rate limiting
├── utils/
│   ├── firestore.ts     # Firestore utilities
│   ├── validation.ts    # Zod schemas
│   └── email.ts         # SendGrid utilities
└── services/
    ├── ai.ts            # AI services
    └── notification.ts  # Push notifications
```

**Example: `lib/middleware/auth.ts`**

```typescript
import { VercelRequest } from '@vercel/node';
import { auth } from 'firebase-admin';
import { initializeApp, getApps, cert } from 'firebase-admin/app';

// Initialize Firebase Admin (singleton)
if (!getApps().length) {
  const serviceAccount = JSON.parse(
    process.env.FIREBASE_SERVICE_ACCOUNT || '{}'
  );
  
  initializeApp({
    credential: cert(serviceAccount),
  });
}

export async function verifyAuth(req: VercelRequest): Promise<string> {
  const authHeader = req.headers.authorization;
  
  if (!authHeader?.startsWith('Bearer ')) {
    throw new Error('Unauthorized: Missing token');
  }

  const token = authHeader.split('Bearer ')[1];
  
  try {
    const decodedToken = await auth().verifyIdToken(token);
    return decodedToken.uid;
  } catch (error) {
    throw new Error('Unauthorized: Invalid token');
  }
}
```

### Bước 6: Environment Variables

Thêm tất cả environment variables vào Vercel:

**Frontend Variables (VITE_*):**
```env
VITE_FIREBASE_API_KEY=...
VITE_FIREBASE_AUTH_DOMAIN=...
VITE_FIREBASE_PROJECT_ID=...
VITE_UPLOADTHING_URL=/api/uploadthing
VITE_UPLOADTHING_APP_ID=...
```

**Backend Variables:**
```env
# Firebase Admin
FIREBASE_SERVICE_ACCOUNT={"type":"service_account",...}

# UploadThing
UPLOADTHING_SECRET=...
UPLOADTHING_APP_ID=...

# AI Services
OPENAI_API_KEY=...
ANTHROPIC_API_KEY=...
GEMINI_API_KEY=...

# Email
SENDGRID_API_KEY=...
SENDGRID_FROM_EMAIL=...

# Payment
STRIPE_SECRET_KEY=...
STRIPE_WEBHOOK_SECRET=...

# Twilio
TWILIO_ACCOUNT_SID=...
TWILIO_AUTH_TOKEN=...

# Cron Jobs
CRON_SECRET=your-secret-key

# URLs
FRONTEND_URL=https://your-domain.vercel.app
VERCEL_API_URL=https://your-domain.vercel.app
```

**Cách thêm vào Vercel:**
1. Vào Project Settings > Environment Variables
2. Add từng variable
3. Chọn environment (Production, Preview, Development)
4. Click "Save"

### Bước 7: Package.json Dependencies

Đảm bảo root `package.json` có tất cả dependencies:

```json
{
  "name": "chatttkrealtimev5",
  "version": "1.0.0",
  "scripts": {
    "dev": "cd frontend && npm run dev",
    "build": "cd frontend && npm run build",
    "vercel-build": "npm run build"
  },
  "dependencies": {
    "@vercel/node": "^3.0.0",
    "firebase-admin": "^12.0.0",
    "uploadthing": "^6.0.0",
    "@uploadthing/server": "^6.0.0",
    "zod": "^3.22.4",
    "openai": "^4.20.1",
    "@anthropic-ai/sdk": "^0.9.1",
    "@sendgrid/mail": "^8.1.0",
    "stripe": "^14.0.0",
    "twilio": "^4.20.0",
    "axios": "^1.6.2"
  }
}
```

### Bước 8: Deploy to Vercel

**Option 1: Deploy via Vercel Dashboard**

1. Vào [Vercel Dashboard](https://vercel.com/)
2. Click "Add New Project"
3. Import GitHub repository
4. Configure:
   - **Framework Preset**: Vite
   - **Root Directory**: `./` (root)
   - **Build Command**: `cd frontend && npm run build`
   - **Output Directory**: `frontend/dist`
   - **Install Command**: `npm install`
5. Add all environment variables
6. Click "Deploy"

**Option 2: Deploy via CLI**

```bash
# Install dependencies
npm install

# Deploy
vercel

# Production deploy
vercel --prod
```

### Bước 9: Verify Deployment

Sau khi deploy, kiểm tra:

1. **Frontend**: `https://your-project.vercel.app`
2. **API Routes**: `https://your-project.vercel.app/api/messages/send`
3. **UploadThing**: `https://your-project.vercel.app/api/uploadthing`
4. **Cron Jobs**: Vào Vercel Dashboard > Settings > Cron Jobs

### Bước 10: Custom Domain (Optional)

1. Vào Project Settings > Domains
2. Add domain của bạn
3. Follow DNS instructions
4. SSL certificate tự động được cấp

### Bước 11: Monitoring & Logs

**View Logs:**
```bash
vercel logs
```

Hoặc trong Vercel Dashboard:
- Vào Project > Functions tab
- Click vào function để xem logs

**Monitor Performance:**
- Vercel Analytics (tự động enable)
- Real-time logs
- Function execution metrics

---

## 🧪 Testing

### Unit Tests

```bash
cd frontend
npm run test:unit
```

### Integration Tests

```bash
# Start emulators first
npm run emulators

# Run tests
npm run test:integration
```

### E2E Tests

```bash
cd frontend
npm run test:e2e:open  # Open Cypress UI
# hoặc
npm run test:e2e      # Run headless
```

---

## 🔧 Troubleshooting

### Lỗi Firebase Emulator

**Problem**: Emulator không start được
**Solution**:
```bash
# Kill existing processes
lsof -ti:8080 | xargs kill -9
lsof -ti:9099 | xargs kill -9
lsof -ti:5001 | xargs kill -9

# Restart emulators
npm run emulators
```

### Lỗi Build Errors

**Problem**: TypeScript errors khi build
**Solution**:
```bash
# Check TypeScript config
cd frontend
npx tsc --noEmit

# Fix errors hoặc update tsconfig.json
```

### Lỗi Deployment

**Problem**: Functions deploy failed
**Solution**:
```bash
# Check Firebase CLI version
firebase --version

# Update Firebase CLI
npm install -g firebase-tools@latest

# Retry deploy
firebase deploy --only functions
```

### Lỗi Permission Denied

**Problem**: Firestore rules deny access
**Solution**:
1. Check Firestore rules trong `firestore/firestore.rules`
2. Verify user authentication
3. Check Custom Claims (admin, godMode)
4. Test rules trong Firebase Console > Firestore > Rules > Rules Playground

### Lỗi UploadThing Upload Failed

**Problem**: File upload không hoạt động
**Solution**:
1. Kiểm tra `UPLOADTHING_SECRET` và `UPLOADTHING_APP_ID` trong environment variables
2. Verify API route `/api/uploadthing` đã được deploy
3. Check browser console để xem lỗi chi tiết
4. Verify file size và type trong file router config
5. Kiểm tra authentication middleware trong upload handler

---

## 📚 Architecture Deep Dive

### Project Structure

```
chatttkrealtimev5/
├── api/                      # Vercel Serverless Functions (Backend)
│   ├── uploadthing/
│   │   ├── core.ts          # UploadThing file router
│   │   └── route.ts         # UploadThing API handler
│   ├── messages/
│   │   └── send.ts          # POST /api/messages/send
│   ├── groups/
│   │   ├── create.ts        # POST /api/groups/create
│   │   └── [id].ts          # GET/PUT/DELETE /api/groups/[id]
│   ├── calls/
│   │   └── start.ts         # POST /api/calls/start
│   ├── stories/
│   │   └── create.ts        # POST /api/stories/create
│   ├── admin/
│   │   └── actions.ts       # POST /api/admin/actions
│   ├── webhooks/
│   │   ├── stripe.ts        # POST /api/webhooks/stripe
│   │   └── twilio.ts        # POST /api/webhooks/twilio
│   └── cron/
│       ├── cleanup-stories.ts
│       ├── generate-analytics.ts
│       ├── backup-database.ts
│       └── send-daily-summary.ts
├── lib/                      # Shared utilities (dùng cho API routes)
│   ├── middleware/
│   │   ├── auth.ts          # Authentication middleware
│   │   └── rateLimit.ts     # Rate limiting
│   ├── utils/
│   │   ├── firestore.ts     # Firestore utilities
│   │   ├── validation.ts    # Zod schemas
│   │   └── email.ts         # SendGrid utilities
│   └── services/
│       ├── ai.ts            # AI services
│       └── notification.ts  # Push notifications
├── frontend/                 # React frontend (Vite)
│   ├── src/
│   │   ├── app/
│   │   │   ├── Router.tsx
│   │   │   ├── Providers.tsx
│   │   │   └── App.tsx
│   │   ├── components/      # UI components
│   │   │   └── upload/      # Upload components
│   │   ├── features/        # Feature modules
│   │   │   ├── chat/        # Chat features
│   │   │   ├── stories/     # Stories features
│   │   │   └── profile/     # Profile features
│   │   ├── lib/             # Frontend utilities
│   │   │   ├── firebase.ts
│   │   │   ├── uploadthing.ts
│   │   │   └── utils.ts
│   │   ├── types/           # TypeScript types
│   │   │   └── uploadthing.ts
│   │   ├── stores/          # Zustand stores
│   │   └── hooks/           # Custom hooks
│   └── package.json
├── functions/                # Firebase Functions (Legacy - có thể giữ cho triggers)
│   └── src/
│       └── triggers/        # Firestore triggers (nếu vẫn dùng Firebase)
│           ├── onUserCreate.ts
│           └── onMessageSent.ts
├── firestore/               # Firestore rules & indexes
├── database/                # Realtime Database rules
├── firebase.json            # Firebase config
├── vercel.json              # Vercel config
├── package.json             # Root package.json
└── README.md
```

### Data Models

**Users:**
```typescript
{
  id: string;
  email: string;
  displayName: string;
  avatar?: string;  // UploadThing URL
  bio?: string;
  isAdmin: boolean;
  godMode: boolean;
  role: 'owner' | 'admin' | 'moderator' | 'member' | 'user';
  permissions: string[];
  friends: string[];
  createdAt: string;
  updatedAt: string;
}
```

**Messages:**
```typescript
{
  id: string;
  conversationId: string;
  senderId: string;
  content: string;
  type: 'text' | 'image' | 'video' | 'file' | 'voice';
  fileUrl?: string;  // UploadThing URL
  fileKey?: string;  // UploadThing file key
  metadata?: {
    fileName?: string;
    fileSize?: number;
    mimeType?: string;
  };
  reactions?: Record<string, Reaction>;
  createdAt: string;
  edited?: boolean;
  deleted?: boolean;
}
```

**Stories:**
```typescript
{
  id: string;
  userId: string;
  mediaUrl: string;  // UploadThing URL
  mediaKey: string;  // UploadThing file key
  mediaType: 'image' | 'video';
  privacy: 'public' | 'friends' | 'private';
  createdAt: string;
  expiresAt: string;  // 24 hours later
}
```

**Groups:**
```typescript
{
  id: string;
  name: string;
  description: string;
  privacy: 'public' | 'private' | 'invite_only';
  avatar?: string;  // UploadThing URL
  ownerId: string;
  admins: string[];
  members: string[];
  memberCount: number;
  createdAt: string;
}
```

### Security Considerations

1. **Firestore Rules**: Luôn verify authentication và ownership
2. **Custom Claims**: Sử dụng để check permissions server-side
3. **Rate Limiting**: Implement trong Cloud Functions
4. **Input Validation**: Sử dụng Zod schema validation
5. **XSS Protection**: Sanitize user input, CSP headers
6. **E2E Encryption**: Optional cho sensitive conversations
7. **UploadThing Security**: 
   - File size limits enforced server-side trong file router
   - File type validation (image, video, pdf, etc.)
   - Authentication middleware trong upload handler (verify Firebase token)
   - CDN với HTTPS tự động
   - Server-side validation trong `onUploadComplete` callback
   - Rate limiting qua UploadThing dashboard (optional)

---

## 📁 UploadThing Implementation Guide

### 1. Upload Avatar (Profile Picture)

**Component Example:**
```typescript
// frontend/src/components/upload/AvatarUpload.tsx
import { UploadButton } from "@/lib/uploadthing";
import { useState } from "react";
import { useToast } from "@/hooks/useToast";

export function AvatarUpload({ userId, currentAvatar }: Props) {
  const [avatarUrl, setAvatarUrl] = useState(currentAvatar);
  const { toast } = useToast();

  return (
    <div>
      <UploadButton
        endpoint="avatarUploader"
        onClientUploadComplete={(res) => {
          if (res && res[0]) {
            const fileUrl = res[0].url;
            setAvatarUrl(fileUrl);
            
            // Update user profile in Firestore
            updateUserAvatar(userId, fileUrl);
            
            toast.success("Avatar uploaded successfully!");
          }
        }}
        onUploadError={(error: Error) => {
          toast.error(`Upload failed: ${error.message}`);
        }}
        content={{
          button: "Upload Avatar",
          allowedContent: "Image (MAX 5MB)",
        }}
      />
      
      {avatarUrl && (
        <img src={avatarUrl} alt="Avatar" className="w-24 h-24 rounded-full" />
      )}
    </div>
  );
}

async function updateUserAvatar(userId: string, avatarUrl: string) {
  const { doc, updateDoc } = await import("firebase/firestore");
  const { db } = await import("@/lib/firebase");
  
  await updateDoc(doc(db, "users", userId), {
    avatar: avatarUrl,
    updatedAt: new Date(),
  });
}
```

### 2. Upload File trong Chat Message

**Component Example:**
```typescript
// frontend/src/components/chat/MessageInput.tsx
import { UploadButton } from "@/lib/uploadthing";
import { sendMessage } from "@/lib/firestore";

export function MessageInput({ conversationId }: Props) {
  const [content, setContent] = useState("");
  const [uploadedFiles, setUploadedFiles] = useState<string[]>([]);

  const handleSendMessage = async () => {
    if (!content.trim() && uploadedFiles.length === 0) return;

    await sendMessage({
      conversationId,
      content,
      type: uploadedFiles.length > 0 ? "image" : "text",
      fileUrl: uploadedFiles[0], // Use first file URL
      metadata: {
        fileCount: uploadedFiles.length,
      },
    });

    setContent("");
    setUploadedFiles([]);
  };

  return (
    <div className="message-input">
      <textarea
        value={content}
        onChange={(e) => setContent(e.target.value)}
        placeholder="Type a message..."
      />
      
      <UploadButton
        endpoint="messageUploader"
        onClientUploadComplete={(res) => {
          if (res) {
            const urls = res.map((file) => file.url);
            setUploadedFiles([...uploadedFiles, ...urls]);
          }
        }}
        onUploadError={(error: Error) => {
          console.error("Upload failed:", error);
        }}
        content={{
          button: "📎 Attach",
          allowedContent: "Images, Videos, Files (MAX 10MB)",
        }}
      />
      
      <button onClick={handleSendMessage}>Send</button>
    </div>
  );
}
```

**Message với File:**
```typescript
// Display message with file
function MessageBubble({ message }: { message: Message }) {
  if (message.type === "image" && message.fileUrl) {
    return (
      <div className="message-bubble">
        <img 
          src={message.fileUrl} 
          alt={message.metadata?.fileName || "Attachment"} 
          className="max-w-md rounded-lg"
        />
        {message.content && <p>{message.content}</p>}
      </div>
    );
  }

  if (message.type === "video" && message.fileUrl) {
    return (
      <div className="message-bubble">
        <video 
          src={message.fileUrl} 
          controls 
          className="max-w-md rounded-lg"
        />
        {message.content && <p>{message.content}</p>}
      </div>
    );
  }

  if (message.type === "file" && message.fileUrl) {
    return (
      <div className="message-bubble">
        <a 
          href={message.fileUrl} 
          target="_blank" 
          rel="noopener noreferrer"
          className="file-link"
        >
          📄 {message.metadata?.fileName || "Download File"}
        </a>
        {message.content && <p>{message.content}</p>}
      </div>
    );
  }

  return <div className="message-bubble">{message.content}</div>;
}
```

### 3. Upload Story

**Component Example:**
```typescript
// frontend/src/components/stories/StoryUpload.tsx
import { UploadDropzone } from "@/lib/uploadthing";
import { useState } from "react";
import { createStory } from "@/lib/firestore";

export function StoryUpload() {
  const [uploadedUrl, setUploadedUrl] = useState<string | null>(null);
  const [privacy, setPrivacy] = useState<"public" | "friends" | "private">("public");

  const handlePublish = async () => {
    if (!uploadedUrl) return;

    await createStory({
      mediaUrl: uploadedUrl,
      mediaType: uploadedUrl.includes("video") ? "video" : "image",
      privacy,
    });

    // Reset and close modal
    setUploadedUrl(null);
  };

  return (
    <div className="story-upload-modal">
      {!uploadedUrl ? (
        <UploadDropzone
          endpoint="storyUploader"
          onClientUploadComplete={(res) => {
            if (res && res[0]) {
              setUploadedUrl(res[0].url);
            }
          }}
          onUploadError={(error: Error) => {
            console.error("Story upload failed:", error);
          }}
          content={{
            button: "Upload Story",
            allowedContent: "Image or Video (MAX 100MB)",
          }}
        />
      ) : (
        <div>
          {uploadedUrl.includes("video") ? (
            <video src={uploadedUrl} controls className="max-w-full" />
          ) : (
            <img src={uploadedUrl} alt="Story" className="max-w-full" />
          )}
          
          <select value={privacy} onChange={(e) => setPrivacy(e.target.value)}>
            <option value="public">Public</option>
            <option value="friends">Friends</option>
            <option value="private">Private</option>
          </select>
          
          <button onClick={handlePublish}>Publish Story</button>
        </div>
      )}
    </div>
  );
}
```

### 4. Upload Group Icon

**Component Example:**
```typescript
// frontend/src/components/groups/GroupIconUpload.tsx
import { UploadButton } from "@/lib/uploadthing";
import { updateGroup } from "@/lib/firestore";

export function GroupIconUpload({ groupId }: { groupId: string }) {
  return (
    <UploadButton
      endpoint="groupIconUploader"
      onClientUploadComplete={async (res) => {
        if (res && res[0]) {
          const iconUrl = res[0].url;
          
          // Update group in Firestore
          await updateGroup(groupId, { avatar: iconUrl });
        }
      }}
      onUploadError={(error: Error) => {
        console.error("Group icon upload failed:", error);
      }}
      content={{
        button: "Upload Group Icon",
        allowedContent: "Image (MAX 5MB)",
      }}
    />
  );
}
```

### 5. Upload Livestream Thumbnail

**Component Example:**
```typescript
// frontend/src/components/livestream/StreamThumbnailUpload.tsx
import { UploadButton } from "@/lib/uploadthing";
import { updateLivestream } from "@/lib/firestore";

export function StreamThumbnailUpload({ streamId }: { streamId: string }) {
  return (
    <UploadButton
      endpoint="livestreamThumbnailUploader"
      onClientUploadComplete={async (res) => {
        if (res && res[0]) {
          const thumbnailUrl = res[0].url;
          
          // Update livestream in Firestore
          await updateLivestream(streamId, { thumbnail: thumbnailUrl });
        }
      }}
      onUploadError={(error: Error) => {
        console.error("Thumbnail upload failed:", error);
      }}
      content={{
        button: "Upload Thumbnail",
        allowedContent: "Image (MAX 10MB)",
      }}
    />
  );
}
```

---

## 🔄 Migration Guide

### Migration 1: Firebase Storage → UploadThing

Migration từ Firebase Storage sang UploadThing đã được hoàn thành. Xem phần "📁 UploadThing Implementation Guide" ở trên.

---

### Migration 2: Firebase Functions → Vercel Serverless Functions

Xem phần chi tiết ở dưới trong "🔄 Migration 2: Firebase Functions → Vercel Serverless Functions" (section riêng).

---

### Bước 1: Backup Dữ Liệu

1. Export tất cả URLs từ Firebase Storage:
```bash
# Sử dụng Firebase Admin SDK để list tất cả files
node scripts/export-storage-urls.js
```

2. Lưu danh sách URLs vào file `storage-backup.json`

### Bước 2: Migrate Files (Optional)

Nếu bạn muốn migrate files từ Firebase Storage sang UploadThing:

```typescript
// scripts/migrate-storage.ts
import { getStorage } from "firebase-admin/storage";
import { uploadFiles } from "@uploadthing/server";

async function migrateFiles() {
  const bucket = getStorage().bucket();
  const [files] = await bucket.getFiles();

  for (const file of files) {
    // Download file từ Firebase Storage
    const [fileBuffer] = await file.download();
    
    // Upload lên UploadThing
    const uploadResult = await uploadFiles({
      files: [new File([fileBuffer], file.name)],
      endpoint: "messageUploader",
    });

    // Update Firestore với URL mới
    const newUrl = uploadResult[0].url;
    await updateFileReference(file.metadata.firebaseStorageDownloadTokens, newUrl);
  }
}
```

### Bước 3: Update Code

1. **Remove Firebase Storage imports:**
```typescript
// ❌ Old
import { getStorage, ref, uploadBytes } from "firebase/storage";

// ✅ New
import { UploadButton } from "@/lib/uploadthing";
```

2. **Update Upload Logic:**
   - Thay `uploadBytes` bằng `UploadButton` hoặc `UploadDropzone`
   - Update file URLs trong Firestore documents

3. **Update Environment Variables:**
   - Remove `VITE_FIREBASE_STORAGE_BUCKET`
   - Add `VITE_UPLOADTHING_URL` và `VITE_UPLOADTHING_APP_ID`

### Bước 4: Test Thoroughly

1. Test upload avatar
2. Test upload message attachments
3. Test upload stories
4. Test upload group icons
5. Verify file URLs trong Firestore

### Bước 5: Cleanup

1. Remove `storage/` folder (không cần storage rules nữa)
2. Remove Firebase Storage từ `firebase.json`
3. Update documentation

---

## 🔄 Migration 2: Firebase Functions → Vercel Serverless Functions

### Overview

Chuyển đổi backend từ Firebase Functions sang Vercel Serverless Functions để:
- Deploy cả frontend và backend trên cùng một platform (Vercel)
- Tận dụng Vercel Edge Network cho performance tốt hơn
- Sử dụng Vercel Cron Jobs cho scheduled tasks
- Unified logging và monitoring

### Migration Strategy

#### 1. Callable Functions → API Routes

**Mapping Table:**

| Firebase Function | Vercel API Route | Method |
|------------------|------------------|--------|
| `sendMessage` | `/api/messages/send` | POST |
| `createGroup` | `/api/groups/create` | POST |
| `startCall` | `/api/calls/start` | POST |
| `reportContent` | `/api/reports/create` | POST |
| `adminActions` | `/api/admin/actions` | POST |
| `sendFriendRequest` | `/api/friends/request` | POST |

**Example Migration:**

**Before (Firebase Functions):**
```typescript
// functions/src/callable/sendMessage.ts
export const sendMessage = onCall(async (request) => {
  const userId = await verifyAuth(request);
  // ... logic
});
```

**After (Vercel API Route):**
```typescript
// api/messages/send.ts
import type { VercelRequest, VercelResponse } from '@vercel/node';
import { verifyAuth } from '../../../lib/middleware/auth';

export default async function handler(
  req: VercelRequest,
  res: VercelResponse
) {
  if (req.method !== 'POST') {
    return res.status(405).json({ error: 'Method not allowed' });
  }

  const userId = await verifyAuth(req);
  // ... same logic
}
```

#### 2. Scheduled Functions → Vercel Cron Jobs

**Mapping Table:**

| Firebase Scheduled | Vercel Cron | Schedule |
|-------------------|-------------|----------|
| `cleanupStories` | `/api/cron/cleanup-stories` | Every hour |
| `generateAnalytics` | `/api/cron/generate-analytics` | Daily at midnight |
| `backupDatabase` | `/api/cron/backup-database` | Weekly (Sunday) |
| `sendDailySummary` | `/api/cron/send-daily-summary` | Daily at 9 AM |

**Example Migration:**

**Before (Firebase Scheduled):**
```typescript
// functions/src/scheduled/cleanupStories.ts
export const cleanupStories = onSchedule(
  { schedule: 'every 1 hours' },
  async () => {
    // ... cleanup logic
  }
);
```

**After (Vercel Cron Job):**
```typescript
// api/cron/cleanup-stories.ts
import type { VercelRequest, VercelResponse } from '@vercel/node';

export default async function handler(
  req: VercelRequest,
  res: VercelResponse
) {
  // Verify cron secret
  if (req.headers.authorization !== `Bearer ${process.env.CRON_SECRET}`) {
    return res.status(401).json({ error: 'Unauthorized' });
  }

  // ... same cleanup logic
  return res.status(200).json({ success: true });
}
```

**Configure trong `vercel.json`:**
```json
{
  "crons": [
    {
      "path": "/api/cron/cleanup-stories",
      "schedule": "0 * * * *"
    }
  ]
}
```

#### 3. Firestore Triggers

**Option A: Keep on Firebase (Recommended)**

Giữ Firestore triggers trên Firebase để xử lý real-time events, nhưng call Vercel API nếu cần:

```typescript
// functions/src/triggers/onMessageSent.ts (Keep this)
export const onMessageSent = onDocumentCreated(
  'conversations/{conversationId}/messages/{messageId}',
  async (event) => {
    // Process locally
    const messageData = event.data?.data();
    
    // Call Vercel API if needed
    await axios.post(`${process.env.VERCEL_API_URL}/api/webhooks/message-sent`, {
      messageData,
    });
  }
);
```

**Option B: Use Event-Driven Architecture**

Sử dụng Firestore webhooks + Vercel API routes:

```typescript
// api/webhooks/firestore-message.ts
export default async function handler(req: VercelRequest, res: VercelResponse) {
  const event = req.body;
  
  if (event.type === 'message.created') {
    await sendNotifications(event.data);
  }
  
  return res.status(200).json({ received: true });
}
```

#### 4. Webhooks → API Routes

**Stripe Webhook:**

```typescript
// api/webhooks/stripe.ts
import Stripe from 'stripe';

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY!);

export default async function handler(
  req: VercelRequest,
  res: VercelResponse
) {
  const sig = req.headers['stripe-signature'] as string;
  
  const event = stripe.webhooks.constructEvent(
    req.body,
    sig,
    process.env.STRIPE_WEBHOOK_SECRET!
  );
  
  // Handle event
  switch (event.type) {
    case 'payment_intent.succeeded':
      await handlePaymentSuccess(event.data.object);
      break;
  }
  
  return res.status(200).json({ received: true });
}
```

### Migration Steps

#### Step 1: Create API Routes Structure

```bash
mkdir -p api/{messages,groups,calls,stories,admin,webhooks,cron}
mkdir -p lib/{middleware,utils,services}
```

#### Step 2: Migrate Shared Code

Copy utilities từ `functions/src/utils/` → `lib/utils/`:

```bash
cp -r functions/src/utils/* lib/utils/
cp -r functions/src/middleware/* lib/middleware/
```

#### Step 3: Update Client Code

**Before (Firebase Functions):**
```typescript
import { getFunctions, httpsCallable } from 'firebase/functions';

const functions = getFunctions();
const sendMessage = httpsCallable(functions, 'sendMessage');

await sendMessage({ conversationId, content });
```

**After (Vercel API):**
```typescript
const response = await fetch('/api/messages/send', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${idToken}`,
  },
  body: JSON.stringify({ conversationId, content }),
});

const data = await response.json();
```

**Create API Client Utility:**

```typescript
// frontend/src/lib/api.ts
import { auth } from './firebase';

async function apiCall<T>(
  endpoint: string,
  options: RequestInit = {}
): Promise<T> {
  const user = auth.currentUser;
  const idToken = await user?.getIdToken();

  const response = await fetch(`/api${endpoint}`, {
    ...options,
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${idToken}`,
      ...options.headers,
    },
  });

  if (!response.ok) {
    const error = await response.json();
    throw new Error(error.message || 'API call failed');
  }

  return response.json();
}

export const api = {
  messages: {
    send: (data: any) => apiCall('/messages/send', {
      method: 'POST',
      body: JSON.stringify(data),
    }),
  },
  groups: {
    create: (data: any) => apiCall('/groups/create', {
      method: 'POST',
      body: JSON.stringify(data),
    }),
  },
  // ... other endpoints
};
```

#### Step 4: Update Environment Variables

Thêm vào Vercel:
- `FIREBASE_SERVICE_ACCOUNT` (JSON stringified)
- `CRON_SECRET` (cho cron jobs)
- Tất cả API keys (OpenAI, Anthropic, SendGrid, etc.)

#### Step 5: Test Locally

```bash
# Install Vercel CLI
npm install -g vercel

# Run locally
vercel dev
```

#### Step 6: Deploy

```bash
# Deploy to Vercel
vercel --prod
```

#### Step 7: Update Frontend API Calls

Thay thế tất cả Firebase Functions calls bằng Vercel API calls.

#### Step 8: Monitor & Debug

- Check Vercel Dashboard > Functions tab
- View logs: `vercel logs`
- Monitor performance metrics

### Benefits of Migration

✅ **Unified Deployment**: Frontend + Backend trên cùng platform  
✅ **Better Performance**: Vercel Edge Network  
✅ **Simpler Architecture**: Tất cả code trong một repo  
✅ **Better DX**: Faster local development với `vercel dev`  
✅ **Cost Effective**: Vercel free tier generous  
✅ **Better Monitoring**: Unified logging và analytics  

### Rollback Plan

Nếu cần rollback:
1. Keep Firebase Functions code trong `functions/` folder
2. Toggle feature flags trong frontend
3. Redeploy Firebase Functions nếu cần

---

## 🎯 Features Guide (User)

### Đăng Ký/Đăng Nhập

1. Truy cập `/auth/register` hoặc `/auth/login`
2. Đăng ký với email/password hoặc social login
3. Nếu email là `khangnek705@gmail.com`, sẽ tự động được cấp quyền admin

### Bắt Đầu Chat

1. Vào `/chat`
2. Tạo conversation mới hoặc chọn conversation có sẵn
3. Gửi tin nhắn, hình ảnh, video, file
4. React với emoji, reply, forward, pin messages

### Upload Files trong Chat

1. Click nút "📎 Attach" trong message input
2. Chọn file từ máy tính
3. File sẽ tự động upload lên UploadThing
4. Tin nhắn sẽ hiển thị file đính kèm

### Video Calls

1. Trong conversation, click nút video call
2. Chọn 1-1 hoặc group call
3. Share screen, toggle mic/camera
4. Sử dụng virtual backgrounds, noise cancellation

### Tạo Stories

1. Vào `/stories`
2. Click "Create Story"
3. Upload ảnh/video từ UploadThing
4. Chọn privacy settings
5. Story tự động xóa sau 24h

### Upload Avatar

1. Vào Profile Settings
2. Click "Upload Avatar"
3. Chọn ảnh từ máy tính
4. Avatar sẽ tự động upload và cập nhật

### Admin Features

1. Truy cập `/admin` (chỉ admin mới thấy)
2. Dashboard: Xem statistics, analytics
3. User Management: Ban/unban users, view activity
4. Content Moderation: Review reports, moderate content
5. System Health: Monitor performance, errors

---

## 📞 Support & Contributing

### Reporting Issues

Tạo issue trên GitHub với:
- Mô tả chi tiết vấn đề
- Steps to reproduce
- Expected vs actual behavior
- Screenshots (nếu có)

### Contributing

1. Fork repository
2. Tạo feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Tạo Pull Request

---

## 📄 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgments

- Firebase team cho nền tảng serverless mạnh mẽ
- UploadThing team cho dịch vụ file upload tuyệt vời (FREE 5GB/tháng)
- React team cho framework tuyệt vời
- Tất cả contributors và users của ChatTTK

---

**Made with ❤️ by ChatTTK Team**
"# Teamchatttkrealtime" 
