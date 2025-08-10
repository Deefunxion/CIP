# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **CIP Interactive Viewer** - a web application that displays Critical Interpretation Protocol documentation in an interactive format. The project consists of a single-page HTML application that dynamically loads and renders multiple markdown documents related to the Critical Interpretation Protocol v3.0.

## Architecture

### Core Structure
- **Single HTML file**: `index.html` - Complete self-contained application
- **Markdown documents**: 4 protocol documents loaded dynamically
- **No build system**: Direct HTML/CSS/JavaScript implementation using CDN resources
- **Client-side rendering**: Uses marked.js for markdown parsing

### Key Components
- **Document grid layout**: 4-panel responsive grid displaying protocol documents
- **Dynamic content loading**: Fetches markdown files via JavaScript
- **Theme system**: Dark/light mode with localStorage persistence  
- **Document interaction**: Copy/download functionality for each document
- **Error handling**: Fallback content for failed document loads

### Dependencies (CDN-based)
- **Tailwind CSS**: Complete utility-first styling framework
- **Marked.js**: Client-side markdown parsing and rendering
- **Inter font**: Typography via Google Fonts

## Technical Implementation

### Document Loading System
The application dynamically loads 4 markdown files:
- `critical_interpretation_protocol_v3.md` - Main CIP v3.0 documentation
- `Speech_Act_Authority.md` - Authority boundaries specification  
- `Agent_Constitution_v3.md` - Enhanced agent identity framework
- `CIP_v3_Implementation_Guide.md` - Technical implementation guide

### JavaScript Architecture
- **Modular functions**: Content loading, rendering, UI interactions
- **Error resilience**: Graceful degradation when documents fail to load
- **Performance optimized**: Concurrent document loading, efficient DOM updates
- **Browser compatibility**: Uses both modern and fallback APIs (Clipboard API with execCommand fallback)

## Development Workflow

### Local Development Setup (Required)
The application must be served via HTTP server due to CORS restrictions when loading markdown files.

#### Quick Setup Options:

**Option 1: Python HTTP Server**
```bash
# Navigate to project directory
cd C:\Users\dee\Desktop\CIP_WEBPAGE

# Python 3.x
python -m http.server 8000

# Python 2.x  
python -m SimpleHTTPServer 8000

# Then open: http://localhost:8000
```

**Option 2: Node.js HTTP Server**
```bash
# Install global server
npm install -g http-server

# Navigate to project directory and run
cd C:\Users\dee\Desktop\CIP_WEBPAGE
http-server -p 8000

# Then open: http://localhost:8000
```

**Option 3: Live Server (VS Code Extension)**
- Install "Live Server" extension in VS Code
- Right-click `index.html` → "Open with Live Server"

### Development Process
- **No build process required**: Edit HTML/CSS/JS directly
- **Real-time updates**: Refresh browser to see changes
- **Document updates**: Edit markdown files, refresh to reload content

### Testing Documents
- Place markdown files in same directory as `index.html`
- Application automatically loads and renders content
- Check browser console for loading errors
- Test copy/download functionality across browsers

## Content Management

### Adding New Documents
1. Add document entry to `DOCS` object in JavaScript:
```javascript
'new-doc': { 
  label: 'Document Title', 
  content: '',
  filename: 'new_document.md'
}
```
2. Create corresponding HTML section in document grid
3. Add file to root directory

### Modifying Existing Documents
- Edit markdown files directly - changes appear on page refresh
- Maintain consistent filename references in JavaScript
- Preserve document structure for proper rendering

## Styling Guidelines

### Design System
- **Utility-first**: Leverages Tailwind CSS class system
- **Responsive**: Mobile-first design with breakpoint-specific layouts
- **Dark mode**: Complete light/dark theme support
- **Typography**: Prose classes for optimal document readability

### Key Style Patterns
- **Cards**: `bg-white dark:bg-neutral-900` with shadow and ring borders
- **Buttons**: Consistent `.btn` classes with ghost/primary variants
- **Typography**: Inter font stack with careful hierarchy
- **Gradients**: Subtle radial gradients for visual enhancement

## Browser Compatibility

### Modern Features Used
- **Fetch API**: Document loading (with error handling)
- **Modern Clipboard API**: Copy functionality with execCommand fallback
- **CSS Grid**: Layout system with flexbox fallbacks
- **CSS Custom Properties**: Theme color management

### Fallback Support
- **Clipboard operations**: Automatic fallback to document.execCommand
- **Fetch failures**: Graceful error messages with troubleshooting guidance
- **CSS degradation**: Progressive enhancement approach

## Security Considerations

### Content Security
- **No external scripts**: Only trusted CDN resources (Tailwind, Marked.js, Google Fonts)
- **Client-side only**: No server-side processing or data transmission
- **Local file access**: Documents loaded from same origin

### Data Handling
- **No data collection**: Application runs entirely client-side
- **localStorage**: Only theme preference stored
- **No external APIs**: Self-contained application

## Performance Optimization

### Loading Strategy
- **Concurrent requests**: All documents loaded in parallel
- **Error resilience**: Failed loads don't block successful ones
- **Efficient rendering**: Direct DOM manipulation, minimal reflows
- **Asset optimization**: CDN resources with compression

### Memory Management
- **Document caching**: Loaded content stored in memory for copy/download
- **Event delegation**: Minimal event listeners
- **No memory leaks**: Clean resource management

## Future Development Notes

### Potential Enhancements
- **Search functionality**: Cross-document text search
- **Section navigation**: Table of contents with anchor links
- **Print optimization**: CSS print media queries  
- **Offline capability**: Service worker for document caching
- **Enhanced responsive**: Better mobile document navigation

### Technical Debt Considerations
- **Single file architecture**: Consider modularization for complex features
- **CDN dependencies**: Evaluate local bundling for offline use
- **Accessibility**: Audit and enhance keyboard navigation, screen reader support
- **Error handling**: More sophisticated retry mechanisms for document loading