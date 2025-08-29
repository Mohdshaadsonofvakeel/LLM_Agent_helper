# Modern Chat Interface

A sleek and responsive chat interface with a modern dark theme design, perfect for AI-powered conversations.

## 🌟 Features

- 🎨 Modern dark theme with vibrant gradient styling
- 💬 Distinct message bubbles for user and assistant
- 🏷️ Clear message labels for better conversation flow
- ✨ Smooth animations and hover effects
- 📱 Fully responsive design for all devices

## 🛠️ Tech Stack

- HTML5
- CSS3 (Modern features):
  - CSS Variables
  - Flexbox
  - Gradients
  - Transitions
- Bootstrap 5.3.3
- Bootstrap Icons

## 📂 Project Structure

```
├── index.html    # Main HTML interface
├── style.css     # Modern dark theme styling
├── agent.js      # Chat functionality
└── vercel.json   # Vercel deployment config
```

## 🚀 Quick Start

### Running Locally

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <project-folder>
   ```

2. Using Python's built-in server:
   ```bash
   python -m http.server 8000
   ```

3. Open your browser and visit:
   ```
   http://localhost:8000
   ```

### Deployment

The project is configured for Vercel deployment with the following features:
- Automatic static file serving
- Proper routing configuration
- Asset optimization

## 💅 Styling Features

### Dark Theme
- Rich dark background with subtle gradients
- High contrast text for readability
- Vibrant accent colors for interactive elements

### Chat Messages
- User messages: Purple/pink gradient theme
- Assistant messages: Cyan/blue gradient theme
- Hover animations for enhanced interactivity
- Clear role labels above messages

### Interface Elements
- Modern input field with custom styling
- Responsive layout adjustments
- Smooth transitions and animations

## 🔧 Customization

You can easily customize the theme by modifying CSS variables in `style.css`:

```css
:root {
  --radius: 16px;
  --bubble-shadow: 0 6px 18px rgba(0, 0, 0, .25);
  --bg-dark: #1a1b26;
  --bg-darker: #16171f;
}
```

## 📱 Responsive Design

- Adapts to different screen sizes
- Mobile-friendly interface
- Optimized message bubbles for small screens
- Maintains readability across devices

## 📄 License

MIT License - Feel free to use this project for your own applications.
