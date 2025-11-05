# EchoChat Frontend

A modern, real-time chat application frontend built with Vue 3, providing a WeChat-like user experience with instant messaging, contact management, and audio/video calling capabilities.

## Project Status

- **Version**: 0.1.0
- **Status**: Active Development
- **Backend API**: Required (see Backend Integration section below)

## Features

### Core Features
- **Real-time Messaging**: One-on-one and group chat support with WebSocket integration
- **Contact Management**: Add, delete, block contacts, and handle friend requests
- **Multiple Message Types**: Support for text, files, audio, and video messages
- **Audio/Video Calling**: WebRTC-based one-on-one audio/video calling with initiate, reject, receive, and hang up functions
- **Session Management**: Chat history and session list management
- **User Profile**: User information management and settings
- **Backend Management**: Administrative interface for premium account users

### User Experience
- Modern and responsive UI built with Element Plus
- Real-time message push via WebSocket
- Offline message handling
- SSL encryption support for secure communication

## Tech Stack

- **Framework**: Vue 3 (Composition API)
- **UI Library**: Element Plus
- **State Management**: Vuex 4
- **Routing**: Vue Router 4
- **HTTP Client**: Axios
- **Real-time Communication**: WebSocket, WebRTC
- **Build Tool**: Vue CLI 5
- **Package Manager**: Yarn

## Project Structure

```
.
├── src/
│   ├── assets/              # Static resources
│   │   ├── css/             # Global styles
│   │   ├── img/             # Images
│   │   └── js/              # Utility scripts
│   ├── components/           # Reusable components
│   │   ├── ContactListModal.vue
│   │   ├── DeleteGroupModal.vue
│   │   ├── DeleteUserModal.vue
│   │   ├── DisableGroupModal.vue
│   │   ├── DisableUserModal.vue
│   │   ├── Modal.vue
│   │   ├── NavigationModal.vue
│   │   ├── SetAdminModal.vue
│   │   ├── SmallModal.vue
│   │   └── VideoModal.vue
│   ├── router/              # Vue Router configuration
│   │   └── index.js
│   ├── store/               # Vuex store
│   │   └── index.js         # API configuration here
│   ├── views/               # Page components
│   │   ├── access/          # Authentication pages
│   │   │   ├── Login.vue
│   │   │   ├── Register.vue
│   │   │   └── SmsLogin.vue
│   │   ├── chat/            # Chat pages
│   │   │   ├── contact/     # Contact chat
│   │   │   │   ├── ContactChat.vue
│   │   │   │   └── ContactList.vue
│   │   │   ├── session/     # Session list
│   │   │   │   └── SessionList.vue
│   │   │   └── user/        # User profile
│   │   │       └── OwnInfo.vue
│   │   └── manager/         # Admin panel
│   │       └── Manager.vue
│   ├── App.vue              # Root component
│   └── main.js              # Application entry point
├── public/                  # Public static files
├── .gitignore
├── babel.config.js          # Babel configuration
├── jsconfig.json            # JavaScript configuration
├── package.json             # Dependencies and scripts
├── vue.config.js            # Vue CLI configuration
└── yarn.lock                # Dependency lock file
```

## Getting Started

### Prerequisites

- Node.js >= 16.x
- Yarn (recommended) or npm
- Backend API server running

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd kama-chat-frontend
   ```

2. **Install dependencies**
   ```bash
   yarn install
   # or
   npm install
   ```

### Development

1. **Start the development server**
   ```bash
   yarn serve
   # or
   npm run serve
   ```

2. **Access the application**
   - Development server runs on `https://localhost:443` (HTTPS)
   - For local development without HTTPS, modify `vue.config.js` to use HTTP on port 8080

### Configuration

#### API Configuration

Configure the backend API endpoints in `src/store/index.js`:

```javascript
state: {
  backendUrl: 'https://your-backend-api.com:8000',
  wsUrl: 'wss://your-backend-api.com:8000',
  // ... other state
}
```

**Note**: Update these URLs to match your backend server address.

#### WebRTC Configuration (Audio/Video Calling)

For audio/video calling to work, you need to configure the TURN server in `src/views/chat/contact/ContactChat.vue`:

```javascript
// Find ICE_CFG configuration
const ICE_CFG = {
  iceServers: [
    {
      urls: 'turn:your-turn-server:3478',
      username: 'your-username',
      credential: 'your-password'
    }
  ]
}

// For local development without TURN server:
// const ICE_CFG = {}
```

#### SSL Certificate Configuration

For HTTPS development, configure SSL certificates in `vue.config.js`:

```javascript
https: {
  // Local development
  cert: fs.readFileSync(path.join(__dirname, 'src/assets/cert/your-cert.pem')),
  key: fs.readFileSync(path.join(__dirname, 'src/assets/cert/your-key.pem')),
  
  // Production server (uncomment for production)
  // cert: fs.readFileSync('/etc/ssl/certs/server.crt'),
  // key: fs.readFileSync('/etc/ssl/private/server.key'),
}
```

## Backend Integration

This frontend requires a compatible backend API. The backend should provide:

- **RESTful API endpoints** for:
  - Authentication (login, register, SMS verification)
  - User management (profile, contacts, groups)
  - Message operations (send, receive, history)
  - Session management
  - Group operations (create, join, leave, manage)
  
- **WebSocket endpoint** for real-time messaging
  - WebSocket URL should be configured in `src/store/index.js`
  - Supports message push, notifications, and real-time updates

- **CORS configuration** to allow requests from the frontend domain

- **SSL/TLS support** for secure connections

### API Endpoint Configuration

Update the following in `src/store/index.js`:

```javascript
backendUrl: 'https://your-backend-api.com:8000',  // REST API base URL
wsUrl: 'wss://your-backend-api.com:8000',         // WebSocket URL
```

## Build

### Production Build

```bash
yarn build
# or
npm run build
```

The production build will be generated in the `dist/` directory.

### Deployment

1. **Build the project**
   ```bash
   yarn build
   ```

2. **Deploy to web server**
   ```bash
   # Copy dist files to web server directory
   sudo cp -r dist/* /var/www/html/
   sudo chmod -R 755 /var/www/html
   sudo chown -R www-data:www-data /var/www/html
   ```

3. **Configure web server (Apache/Nginx)**
   - Ensure HTTPS is enabled
   - Configure SSL certificates
   - Set up proper CORS headers if needed
   - Configure reverse proxy for API requests if needed

## Scripts

- `yarn serve` - Start development server
- `yarn build` - Build for production
- `yarn lint` - Run ESLint

## Development Guidelines

### Code Style
- Follow Vue 3 Composition API best practices
- Use ESLint for code linting
- Maintain consistent component structure

### Component Structure
- Use Vue 3 Composition API (`<script setup>`)
- Keep components focused and reusable
- Separate business logic from presentation

### State Management
- Use Vuex for global state management
- Keep local state in components when possible
- API configuration is stored in `src/store/index.js`

### Routing
- Define routes in `src/router/index.js`
- Use route guards for authentication

## Security Considerations

- All API communications should use HTTPS
- WebSocket connections are encrypted (WSS)
- SSL certificates required for production
- Implement proper authentication and authorization
- Store sensitive configuration in environment variables (consider migration)

## Notes

- **This is a frontend-only repository**. A separate backend API server is required for full functionality.
- The backend API should provide WebSocket endpoints for real-time messaging
- WebRTC features require proper TURN server configuration for NAT traversal
- Ensure backend CORS is configured to allow frontend origin
- For production, update API endpoints and WebRTC configurations in the respective files
- Consider using environment variables for API configuration in future versions

## Contributing

1. Follow the existing code style
2. Test your changes thoroughly
3. Update documentation as needed
4. Ensure backend API compatibility

## License

[MIT License](LICENSE) - See LICENSE file for details

## Application Preview

<img width="1831" height="1097" alt="image" src="https://github.com/user-attachments/assets/39f1584f-f0f4-43de-8025-27a9546c19e2" />

<img width="1815" height="1085" alt="image" src="https://github.com/user-attachments/assets/4090ca8c-aaa6-43fc-8d4e-588916783db7" />


