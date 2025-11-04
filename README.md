# EchoChat Frontend

A real-time chat application frontend built with Vue 3, providing a WeChat-like user experience with instant messaging, contact management, and audio/video calling capabilities.

## ✨ Features

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

## 🛠️ Tech Stack

- **Framework**: Vue 3 (Composition API)
- **UI Library**: Element Plus
- **State Management**: Vuex 4
- **Routing**: Vue Router 4
- **HTTP Client**: Axios
- **Real-time Communication**: WebSocket, WebRTC
- **Build Tool**: Vue CLI 5
- **Package Manager**: Yarn

## 📁 Project Structure

```
chat-server/
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
│   │   └── index.js
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

## 🚀 Getting Started

### Prerequisites

- Node.js >= 16.x
- Yarn (recommended) or npm
- Backend API server running

### Installation

1. **Clone the repository**
   ```bash
   cd web/chat-server
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

#### API Configuration

Update the backend API base URL in your API service files (typically in `src/store/index.js` or API utility files).

#### SSL Certificate Configuration

For HTTPS development, configure SSL certificates in `vue.config.js`:

```javascript
https: {
  // Local development
  cert: fs.readFileSync(path.join(__dirname, 'src/assets/cert/your-cert.pem')),
  key: fs.readFileSync(path.join(__dirname, 'src/assets/cert/your-key.pem')),
  
  // Production server
  // cert: fs.readFileSync('/etc/ssl/certs/server.crt'),
  // key: fs.readFileSync('/etc/ssl/private/server.key'),
}
```

## 📦 Build

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

## 🧪 Scripts

- `yarn serve` - Start development server
- `yarn build` - Build for production
- `yarn lint` - Run ESLint

## 🔧 Development Guidelines

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

### Routing
- Define routes in `src/router/index.js`
- Use route guards for authentication

## 🔐 Security Considerations

- All API communications should use HTTPS
- WebSocket connections are encrypted
- SSL certificates required for production
- Implement proper authentication and authorization

## 📝 Notes

- The application requires a running backend API server
- WebRTC features require proper TURN server configuration for NAT traversal
- Ensure backend CORS is configured to allow frontend origin
- For production, update API endpoints and WebRTC configurations

## 🤝 Contributing

1. Follow the existing code style
2. Test your changes thoroughly
3. Update documentation as needed

## 📄 License

See the main project LICENSE file for details.

