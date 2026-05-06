# Video Editor

A Node.js-based video editing application that allows users to upload, process, and manipulate video files through a web interface.

## Features

- **User Authentication**: Login/logout system with session management
- **Video Upload**: Upload video files to the platform
- **Video Processing**:
  - Extract audio from videos
  - Resize videos to different dimensions
  - Generate thumbnails
- **Cluster Mode**: Multi-core processing for efficient video handling
- **Job Queue**: Asynchronous video processing with queue management

## Tech Stack

- **Backend**: Node.js with CPeach framework
- **Video Processing**: FFmpeg/FFprobe
- **Storage**: File-based JSON database
- **Frontend**: HTML5, CSS3, JavaScript
- **Architecture**: Multi-process clustering with job queue

## Project Structure

```
video-editor/
├── src/
│   ├── controllers/          # Route controllers
│   │   ├── user.js          # User management
│   │   └── video.js         # Video operations
│   ├── middleware/          # Express middleware
│   ├── DB.js               # Database layer
│   ├── router.js           # API routes
│   ├── index.js            # Main server file
│   └── cluster.js          # Cluster management
├── lib/
│   ├── JobQueue.js         # Video processing queue
│   ├── FF.js              # FFmpeg operations
│   └── util.js            # Utility functions
├── public/                 # Static assets
│   ├── index.html
│   ├── scripts.js
│   └── styles.css
├── data/                   # JSON data files
│   ├── users
│   ├── videos
│   └── sessions
└── storage/               # Video file storage
```

## API Endpoints

### User Routes

- `POST /api/login` - User authentication
- `DELETE /api/logout` - User logout
- `GET /api/user` - Get user information
- `PUT /api/user` - Update user information

### Video Routes

- `GET /api/videos` - List user's videos
- `POST /api/upload-video` - Upload new video
- `PATCH /api/video/extract-audio` - Extract audio from video
- `PUT /api/video/resize` - Resize video dimensions
- `GET /get-video-asset` - Serve video assets

## Installation

1. Clone the repository

```bash
git clone https://github.com/vasylpryimakdev/node-js-video-editor.git

cd node-js-video-editor
```

2. Install dependencies:

```bash
npm install
```

3. Ensure FFmpeg is installed on your system and available in PATH

## Usage

### Development Mode

```bash
npm start
```

Server runs on port 8060

### Cluster Mode (Production)

```bash
npm run cluster
```

Runs multiple worker processes based on available CPU cores

## Video Processing Features

### Supported Operations

- **Thumbnail Generation**: Creates thumbnails at 5 seconds into video
- **Audio Extraction**: Extracts audio track without re-encoding
- **Video Resizing**: Changes video dimensions while preserving quality
- **Dimension Detection**: Automatically detects video dimensions

### Processing Queue

- Videos are processed asynchronously using a job queue
- Failed jobs are automatically cleaned up
- Processing status is tracked in the database

## Database

The application uses a file-based JSON database with three main collections:

- **users**: User accounts and authentication
- **videos**: Video metadata and processing status
- **sessions**: Active user sessions

## Default Users

The system comes with pre-configured test users:

- Username: `liam23`, Password: `string`
- Username: `merit.sky`, Password: `string`
- Username: `ben.poet`, Password: `string`

## Architecture

### Multi-Process Clustering

- Primary process manages job queue
- Worker processes handle HTTP requests
- Automatic worker restart on failure

### Job Processing

- Video resize jobs are queued and processed sequentially
- Jobs survive server restarts
- Processing status is persisted

## Dependencies

- **cpeak**: Web framework for Node.js
- **node:cluster**: Built-in clustering support
- **node:child_process**: FFmpeg/FFprobe execution

## Requirements

- Node.js (v16+)
- FFmpeg/FFprobe installed and in PATH
- Sufficient disk space for video storage
