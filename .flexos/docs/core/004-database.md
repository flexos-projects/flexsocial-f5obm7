---
id: database
title: Database Schema
description: The proposed data models and collections for the flexSocial application.
type: doc
subtype: core
status: draft
sequence: 4
tags:
  - database
  - schema
  - technical
createdAt: "2023-10-27T10:00:00.000Z"
updatedAt: "2023-10-27T10:00:00.000Z"
---

This document outlines the preliminary database schema for flexSocial. We will use a NoSQL document database (like MongoDB or Firestore) to accommodate the flexible and nested nature of our data. All collections are designed with user data isolation in mind, typically partitioned by `userId`.

### Core Collections

**1. `users`**

Stores essential user account information.

```json
{
  "_id": "userId_abc123",
  "email": "artist@example.com",
  "hashedPassword": "...",
  "displayName": "John Artist",
  "profileImageUrl": "...",
  "subscription": {
    "plan": "pro",
    "status": "active",
    "endDate": "2024-11-27T10:00:00Z"
  },
  "createdAt": "2023-10-27T10:00:00Z",
  "updatedAt": "..."
}
```

**2. `personas`**

Stores the configuration and knowledge base for a user's AI persona. Each user has one primary persona document.

```json
{
  "_id": "personaId_def456",
  "userId": "userId_abc123",
  "knowledgeSources": [
    { "type": "url", "value": "https://my-art-blog.com", "status": "processed" },
    { "type": "file", "storagePath": "/brand_guide.pdf", "status": "processed" },
    { "type": "text", "value": "My core mission is to...", "status": "processed" }
  ],
  "styleConfiguration": {
    "goal": "establish_thought_leadership",
    "tone": {
      "formality": 0.8, // 0=casual, 1=professional
      "humor": 0.2,
      "complexity": 0.7
    },
    "emojiUsage": "low"
  },
  "coreHashtags": ["#DigitalArt", "#CreativeCoding", "#AIart"],
  "visuals": {
    "logoUrl": "...",
    "colorPalette": ["#10b981", "#0f172a", "#ffffff"]
  },
  "updatedAt": "..."
}
```

**3. `raw_content`**

This collection holds every piece of content the user inputs into "The Stream".

```json
{
  "_id": "rawId_ghi789",
  "userId": "userId_abc123",
  "type": "url", // url, text, image, video
  "sourceValue": "https://techcrunch.com/some-article",
  "intent": "disagree", // agree, disagree, promote
  "intensity": 4, // 1 to 5
  "userContext": "I think the author misses the point about decentralized AI...",
  "status": "processed", // pending, processing, processed
  "createdAt": "..."
}
```

**4. `flexes`**

Stores the generated post stubs (Flexes) created by the AI from `raw_content`.

```json
{
  "_id": "flexId_jkl012",
  "userId": "userId_abc123",
  "rawContentId": "rawId_ghi789",
  "status": "for_review", // draft, for_review, scheduled, published, discarded
  "baseSummary": "A critical take on the new TechCrunch article about AI...",
  "platformOptimizations": [
    {
      "platform": "twitter", // twitter, linkedin, instagram
      "content": "Short thread disagreeing with the latest TC article on AI. They claim X, but the reality is Y. 1/3",
      "mediaUrls": [],
      "hashtags": ["#AI", "#TechCritique"]
    },
    {
      "platform": "linkedin",
      "content": "A thoughtful analysis of the recent TechCrunch piece... While the article makes some valid points, it overlooks the critical impact of decentralized AI models. Here's my perspective...",
      "mediaUrls": ["/generated_quote_graphic.png"],
      "hashtags": ["#ArtificialIntelligence", "#Technology", "#FutureTech"]
    }
  ],
  "createdAt": "..."
}
```

**5. `scheduled_posts`**

Holds the final, user-approved posts that are scheduled for publishing.

```json
{
  "_id": "postId_mno345",
  "userId": "userId_abc123",
  "flexId": "flexId_jkl012",
  "platform": "linkedin",
  "content": "A thoughtful analysis...",
  "mediaUrls": ["/generated_quote_graphic.png"],
  "scheduledAt": "2023-11-05T14:00:00Z",
  "status": "scheduled", // scheduled, posted, failed
  "postResult": {
    "postId": "linkedin_postId_xyz",
    "postUrl": "..."
  }
}
```

**6. `social_connections`**

Securely stores OAuth tokens and connection details for user's social media accounts.

```json
{
  "_id": "connId_pqr678",
  "userId": "userId_abc123",
  "platform": "twitter",
  "username": "@johnartist",
  "profileId": "twitter_profile_id",
  "encryptedAccessToken": "...",
  "encryptedRefreshToken": "...",
  "expiresAt": "...",
  "status": "active", // active, expired
  "createdAt": "..."
}
```

**7. `vectors`**

This is a specialized collection, likely in a dedicated vector database like Pinecone or Weaviate, storing the embeddings of the user's persona knowledge base for efficient AI retrieval.

```json
{
  "_id": "vecId_stu901",
  "userId": "userId_abc123",
  "personaId": "personaId_def456",
  "sourceType": "url",
  "sourceValue": "https://my-art-blog.com/about",
  "chunkText": "A snippet of text from the about page...",
  "embedding": [0.0123, -0.0456, ... ] // High-dimensional vector
}
```