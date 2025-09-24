# Yggdraz Editor

A modern, feature-rich WYSIWYG rich-text editor for Nuxt.js applications, built on top of Tiptap and Nuxt UI V3. This editor provides a comprehensive set of tools for creating rich content with advanced features like AI assistance, collaboration, and extensive formatting options.

## Features

### ✨ Core Features
- **Modern WYSIWYG Interface**: Clean, intuitive editor with bubble menus and toolbar
- **Rich Text Formatting**: Bold, italic, underline, strikethrough, superscript, subscript
- **Typography**: Multiple heading levels, font families, font sizes, text colors
- **Lists & Structure**: Bullet lists, ordered lists, task lists, blockquotes
- **Advanced Formatting**: Text alignment, highlighting, code blocks, horizontal rules
- **Media Support**: Images, videos, iframes, emojis
- **Tables**: Full table support with cell formatting and manipulation
- **AI Integration**: Built-in AI assistance for content generation and enhancement
- **Collaboration**: Real-time collaborative editing with cursor tracking
- **Comments**: Add, edit, and manage comments on content
- **Export/Import**: Multiple format support including Word document import
- **Accessibility**: Speech recognition and text-to-speech support
- **Drawing**: Built-in drawing/paper functionality
- **Search & Replace**: Advanced search and replace capabilities
- **Full-screen Mode**: Distraction-free editing experience

### 🎨 UI Components
- **Bubble Menus**: Context-sensitive menus that appear on text selection
- **Toolbar**: Comprehensive toolbar with all formatting options
- **Slash Commands**: Quick insertion of elements using `/` commands
- **Drag Handles**: Easy content manipulation and reordering
- **Responsive Design**: Works seamlessly across all device sizes

## Installation

### Prerequisites
- Node.js 18+ 
- Nuxt.js 3.x
- pnpm (recommended) or npm

### Install the Package

```bash
# Using pnpm (recommended)
pnpm add @yggdraz/editor

# Using npm
npm install @yggdraz/editor

# Using yarn
yarn add @yggdraz/editor
```

### Add to Your Nuxt Project

1. **Add the module to your `nuxt.config.ts`:**

```typescript
export default defineNuxtConfig({
  modules: [
    '@yggdraz/editor'
  ]
})
```

2. **Configure runtime config (optional):**

```typescript
export default defineNuxtConfig({
  runtimeConfig: {
    public: {
      // AI Configuration
      OPENAI_API_KEY: process.env.NUXT_OPENAI_API_KEY,
      
      // Export Configuration  
      CONVERT_APP_ID: process.env.NUXT_CONVERT_APP_ID,
      JWT_CONVERT_TOKEN: process.env.NUXT_JWT_CONVERT_TOKEN,
      
      // Media APIs
      UNSPLASH_API_KEY: process.env.NUXT_UNSPLASH_API_KEY,
      PIXABAY_API_KEY: process.env.NUXT_PIXABAY_API_KEY,
      PEXELS_API_KEY: process.env.NUXT_PEXELS_API_KEY,
      GIPHY_API_KEY: process.env.NUXT_GIPHY_API_KEY,
      
      // Collaboration
      WEBSOCKET_URL: process.env.NUXT_WEBSOCKET_URL
    }
  }
})
```

## Basic Usage

### Simple Editor

```vue
<template>
  <div>
    <YggdrazEditor v-model="content" />
  </div>
</template>

<script setup>
const content = ref('<p>Start typing your content here...</p>')
</script>
```

### Advanced Configuration

```vue
<template>
  <YggdrazEditor
    v-model="content"
    :max-width="800"
    :min-height="400"
    output="json"
    :debounce="true"
    :debounce-delay="1000"
    @change="handleChange"
    @comment:added="handleCommentAdded"
  />
</template>

<script setup>
const content = ref({
  type: 'doc',
  content: [
    {
      type: 'paragraph',
      content: [
        { type: 'text', text: 'Hello World!' }
      ]
    }
  ]
})

const handleChange = ({ editor, output }) => {
  console.log('Content changed:', output)
}

const handleCommentAdded = (comment) => {
  console.log('Comment added:', comment)
}
</script>
```

## API Reference

### Component Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `modelValue` | `string \| object` | `''` | The editor content (HTML string or JSON object) |
| `output` | `'html' \| 'json' \| 'text'` | `'html'` | Output format for the content |
| `dense` | `boolean` | `false` | Enable dense mode for compact UI |
| `disabled` | `boolean` | `false` | Disable the editor |
| `label` | `string` | `undefined` | Label for the editor |
| `hideToolbar` | `boolean` | `false` | Hide the toolbar |
| `disableBubble` | `boolean` | `false` | Disable bubble menus |
| `hideBubble` | `boolean` | `false` | Hide bubble menus completely |
| `removeDefaultWrapper` | `boolean` | `false` | Remove default wrapper from output |
| `maxWidth` | `string \| number` | `undefined` | Maximum width of the editor |
| `minHeight` | `string \| number` | `undefined` | Minimum height of the editor |
| `maxHeight` | `string \| number` | `undefined` | Maximum height of the editor |
| `extensions` | `AnyExtension[]` | `[]` | Additional Tiptap extensions |
| `debounce` | `boolean` | `true` | Enable debounced updates |
| `debounceDelay` | `number` | `5000` | Debounce delay in milliseconds |
| `editorClass` | `string \| string[] \| object` | `undefined` | CSS classes for the editor |
| `contentClass` | `string \| string[] \| object` | `undefined` | CSS classes for the content area |

### Events

| Event | Payload | Description |
|-------|---------|-------------|
| `update:modelValue` | `string \| object` | Emitted when content changes |
| `change` | `{ editor, output }` | Emitted when content changes (debounced) |
| `selectionUpdate` | `Editor` | Emitted when text selection changes |
| `enter` | `void` | Emitted when Enter key is pressed |
| `blur` | `void` | Emitted when editor loses focus |
| `destroy` | `void` | Emitted when editor is destroyed |
| `comment:added` | `object` | Emitted when a comment is added |
| `comment:deleted` | `number` | Emitted when a comment is deleted |
| `comment:updated` | `object` | Emitted when a comment is updated |
| `comment:replied` | `object` | Emitted when a comment is replied to |

## Extensions & Features

### BaseKit Extensions

The editor comes with a comprehensive set of extensions through the `BaseKit`. You can configure which extensions to enable:

```typescript
import { BaseKit } from '@yggdraz/editor'

// Configure specific extensions
const customExtensions = [
  BaseKit.configure({
    // Disable specific features
    ai: false,
    collaboration: false,
    comment: false,
    
    // Configure specific extensions
    heading: {
      levels: [1, 2, 3] // Only allow H1, H2, H3
    },
    
    color: {
      types: ['text', 'background'] // Enable text and background colors
    },
    
    image: {
      inline: true,
      allowBase64: true
    }
  })
]
```

### Available Extensions

#### Text Formatting
- **Bold** (`bold`): Bold text formatting
- **Italic** (`italic`): Italic text formatting  
- **Underline** (`underline`): Underlined text
- **Strikethrough** (`strike`): Strikethrough text
- **Superscript** (`superscript`): Superscript text
- **Subscript** (`subscript`): Subscript text
- **Code** (`code`): Inline code formatting
- **Highlight** (`highlight`): Text highlighting

#### Typography
- **Heading** (`heading`): Multiple heading levels (H1-H6)
- **Font Family** (`fontFamily`): Font family selection
- **Font Size** (`fontSize`): Font size control
- **Text Color** (`color`): Text and background colors
- **Text Align** (`textAlign`): Text alignment options

#### Structure
- **Paragraph** (`paragraph`): Basic paragraph formatting
- **Blockquote** (`blockquote`): Quote blocks
- **Horizontal Rule** (`horizontalRule`): Divider lines
- **Hard Break** (`hardBreak`): Line breaks

#### Lists
- **Bullet List** (`bulletList`): Unordered lists
- **Ordered List** (`orderedList`): Numbered lists  
- **Task List** (`taskList`): Checkbox lists
- **List Item** (`listItem`): Individual list items

#### Media
- **Image** (`image`): Image insertion and management
- **Image Upload** (`imageUpload`): Drag & drop image uploads
- **Iframe** (`iframe`): Embedded iframes
- **YouTube** (`youtube`): YouTube video embeds
- **Emoji** (`emoji`): Emoji picker and insertion

#### Advanced Features
- **Table** (`table`): Full table support with cells, headers, rows
- **Code Block** (`codeBlock`): Syntax-highlighted code blocks
- **Details** (`details`): Collapsible content sections
- **Columns** (`columns`): Multi-column layouts
- **Alert** (`alert`): Alert boxes with different types
- **Paper** (`paper`): Drawing/annotation functionality

#### AI & Collaboration
- **AI** (`ai`): AI-powered content generation
- **Collaboration** (`collaboration`): Real-time collaborative editing
- **Collaboration Cursor** (`collaborationCursor`): User cursor tracking
- **Comment** (`comment`): Comment system

#### Utility Features
- **History** (`history`): Undo/redo functionality
- **Character Count** (`characterCount`): Word and character counting
- **Focus** (`focus`): Focus management
- **Fullscreen** (`fullScreen`): Fullscreen editing mode
- **Export** (`export`): Content export functionality
- **Import** (`import`): Content import functionality
- **Format Painter** (`formatPainter`): Copy/paste formatting
- **Search & Replace** (`searchReplace`): Find and replace text

## Examples

### Blog Post Editor

```vue
<template>
  <div class="blog-editor">
    <YggdrazEditor
      v-model="postContent"
      :max-width="800"
      :min-height="500"
      output="html"
      @change="saveDraft"
    />
  </div>
</template>

<script setup>
const postContent = ref('<h1>My Blog Post</h1><p>Start writing...</p>')

const saveDraft = ({ output }) => {
  // Auto-save functionality
  localStorage.setItem('blog-draft', output)
}
</script>
```

### Collaborative Document Editor

```vue
<template>
  <div class="collaborative-editor">
    <YggdrazEditor
      v-model="documentContent"
      :extensions="collaborativeExtensions"
      :max-width="1000"
    />
  </div>
</template>

<script setup>
import * as Y from 'yjs'
import { WebsocketProvider } from 'y-websocket'

const ydoc = new Y.Doc()
const provider = new WebsocketProvider('ws://localhost:1234', 'document-room', ydoc)

const collaborativeExtensions = [
  BaseKit.configure({
    collaboration: {
      document: ydoc
    },
    collaborationCursor: {
      provider: provider
    },
    comment: true
  })
]

const documentContent = ref({})
</script>
```

### Minimal Editor

```vue
<template>
  <YggdrazEditor
    v-model="content"
    :hide-toolbar="false"
    :extensions="minimalExtensions"
  />
</template>

<script setup>
const minimalExtensions = [
  BaseKit.configure({
    // Only basic formatting
    bold: true,
    italic: true,
    heading: { levels: [1, 2, 3] },
    bulletList: true,
    orderedList: true,
    
    // Disable advanced features
    ai: false,
    collaboration: false,
    comment: false,
    image: false,
    table: false
  })
]
</script>
```

## Customization

### Custom Extensions

You can add your own Tiptap extensions:

```vue
<template>
  <YggdrazEditor
    v-model="content"
    :extensions="customExtensions"
  />
</template>

<script setup>
import { Extension } from '@tiptap/core'

const customExtensions = [
  Extension.create({
    name: 'customExtension',
    addCommands() {
      return {
        customCommand: () => ({ commands }) => {
          // Your custom command logic
          return true
        }
      }
    }
  })
]
</script>
```

### Styling

The editor uses CSS custom properties for theming. You can override the default styles:

```css
/* Custom editor styles */
.yggdraz-editor {
  --editor-bg: #ffffff;
  --editor-text: #333333;
  --editor-border: #e5e5e5;
  --editor-focus: #3b82f6;
}

/* Dark mode support */
.dark .yggdraz-editor {
  --editor-bg: #1a1a1a;
  --editor-text: #ffffff;
  --editor-border: #404040;
  --editor-focus: #60a5fa;
}
```

## Advanced Features

### AI Integration

Enable AI features by providing an OpenAI API key:

```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  runtimeConfig: {
    public: {
      OPENAI_API_KEY: process.env.NUXT_OPENAI_API_KEY
    }
  }
})
```

```vue
<template>
  <YggdrazEditor
    v-model="content"
    :extensions="aiExtensions"
  />
</template>

<script setup>
const aiExtensions = [
  BaseKit.configure({
    ai: {
      // AI configuration options
      model: 'gpt-4',
      temperature: 0.7
    }
  })
]
</script>
```

### Collaboration

Enable real-time collaboration:

```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  runtimeConfig: {
    public: {
      WEBSOCKET_URL: process.env.NUXT_WEBSOCKET_URL
    }
  }
})
```

```vue
<template>
  <YggdrazEditor
    v-model="content"
    :extensions="collaborationExtensions"
  />
</template>

<script setup>
const collaborationExtensions = [
  BaseKit.configure({
    collaboration: {
      document: ydoc // Yjs document
    },
    collaborationCursor: {
      provider: provider // WebSocket provider
    }
  })
]
</script>
```

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## Contributing

We welcome contributions! Please see our contributing guidelines for details.

## License

MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support and questions:
- Create an issue on GitHub
- Check the documentation
- Join our community discussions

---

Built with ❤️ using [Tiptap](https://tiptap.dev/) and [Nuxt UI](https://ui.nuxt.com/)

## Credits

Special thanks to [@Achraf931](https://github.com/Achraf931) and the [leazy-editor](https://github.com/leazyhub/leazy-editor) project that served as the foundation for this editor. This project builds upon their excellent work and extends it with additional features and improvements.
