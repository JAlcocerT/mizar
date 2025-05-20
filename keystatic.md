# Keystatic Integration in Mizar Astro Theme

This document explains how [Keystatic](https://keystatic.com) has been integrated into the Mizar Astro theme, providing a powerful headless content management system (CMS) for the website.

## What is Keystatic?

Keystatic is a modern, open-source headless CMS that works with your git workflow. It provides an intuitive admin interface for content editors while storing content as files directly in your repository, allowing developers to work with content using their preferred tools.

Key benefits of Keystatic:
- **Git-based**: Content is stored as markdown and JSON files in your git repository
- **Developer-friendly**: No database or external services required
- **Editor-friendly**: Beautiful, intuitive UI for content editors
- **Type-safe**: First-class TypeScript support
- **Zero vendor lock-in**: Your content stays in your repository

## Basic Integration with Astro

### 1. Package Installation

The theme incorporates Keystatic through the following NPM packages:

```json
{
  "@keystatic/astro": "^5.0.0",
  "@keystatic/core": "^0.5.17",
  "keystatic-components": "^0.0.2"
}
```

### 2. Astro Configuration

Keystatic is integrated as an Astro integration in the `astro.config.ts` file:

```typescript
import keystatic from "@keystatic/astro";

export default defineConfig({
  // other config...
  redirects: {
    "/admin": "/keystatic",
  },
  integrations: [
    // other integrations...
    keystatic(),
    // more integrations...
  ],
  // PWA config excludes Keystatic routes
  workbox: {
    navigateFallbackDenylist: [/^\/keystatic/, /^\/api/],
  }
});
```

This setup:
- Integrates Keystatic with Astro
- Redirects `/admin` to `/keystatic` for easier admin access
- Configures service worker to exclude Keystatic routes

## Content Structure in Keystatic

The Mizar theme uses Keystatic to manage several types of content, configured in `keystatic.config.ts`:

### Storage Configuration

```typescript
export default config({
  storage: {
    kind: "local",
  },
  // rest of configuration...
});
```

This configures Keystatic to use local file storage, meaning content is stored directly in the repository.

### Admin UI Customization

```typescript
ui: {
  brand: {
    name: "Your Company",
    mark: BrandMarkComponent,
  },
},
```

This customizes the Keystatic admin interface with the site's branding.

### Content Types

The theme defines two main types of content structures:

#### 1. Singletons

Singletons are used for unique content that only has one instance, such as:

- **Header**: Navigation menu, logo, and contact information
- **Footer**: Footer content, social links, and copyright information
- **Widget**: WhatsApp widget configuration

Example of the header singleton:
```typescript
header: singleton({
  label: "Navigation",
  path: "src/content/global/header",
  format: { data: "json" },
  schema: {
    logo: fields.object({
      // logo fields...
    }),
    pages: fields.array(
      // pages array config...
    ),
    // other header fields...
  },
}),
```

#### 2. Collections

Collections are used for repeatable content types, such as:

- **Pages**: Website pages with customizable content
- **Posts**: Blog articles
- **Works**: Portfolio/case studies
- **Authors**: Content creators' information

Example of the posts collection:
```typescript
posts: collection({
  label: "Posts",
  slugField: "title",
  path: "src/content/posts/it/*",
  entryLayout: "content",
  columns: ["title", "lastUpdateDate"],
  previewUrl: "/blog/{slug}",
  format: { contentField: "content" },
  schema: {
    // post fields definition...
  },
}),
```

## Content Field Types

Keystatic provides various field types to structure content:

- **Text fields**: For titles, descriptions, and simple content
- **Rich text/Markdoc fields**: For formatted content with components
- **Image fields**: For media uploads with directory configuration
- **Select fields**: For predefined options
- **Relationship fields**: For connecting content pieces (like authors to posts)
- **Date fields**: For publication and update dates
- **Arrays**: For repeatable sections like tags or features

## Accessing the Admin Interface

Content editors can access the Keystatic admin interface at:
- `/keystatic` - Main admin URL
- `/admin` - Redirects to `/keystatic` for convenience

The admin interface provides:
- Content editing for all defined collections and singletons
- Rich text editing with custom components
- Media management
- Content previewing

## Content Usage in Astro Components

The content managed through Keystatic is stored in the `src/content` directory and can be accessed in Astro components using Astro's content collections API:

```astro
---
// Example of accessing blog posts
import { getCollection } from 'astro:content';
const posts = await getCollection('posts');
---

<ul>
  {posts.map(post => (
    <li>
      <a href={`/blog/${post.slug}`}>{post.data.title}</a>
      <p>Published: {post.data.pubDate.toLocaleDateString()}</p>
    </li>
  ))}
</ul>
```

## Development Workflow with Keystatic

1. **Local Development**: When running `astro dev`, Keystatic is available at `http://localhost:4321/keystatic/`
2. **Content Creation**: Add or edit content through the Keystatic UI
3. **Content Storage**: Changes are saved as files in the `src/content` directory
4. **Version Control**: Commit content changes alongside code changes
5. **Deployment**: Content is built together with the site during the build process

## Custom Components in Keystatic

The theme extends Keystatic with custom components for rich content editing:

- Container components
- Layout components (Flex, Grid)
- Feature display components
- Media components

These components are defined in the Keystatic config and available in the content editor.

## Production Considerations

When deploying to production, there are a few important considerations:

1. **Authentication**: Configure authentication for the Keystatic admin interface
2. **GitHub Integration**: Optionally configure GitHub integration for content editing
3. **Build Process**: Ensure your build process includes Keystatic content

## Extending Keystatic

To extend the current Keystatic implementation:

1. **Add New Collections**: Define new content types in `keystatic.config.ts`
2. **Create Custom Components**: Develop new components for the editor
3. **Configure Media Directories**: Set up directories for image uploads
4. **Adjust Schema**: Modify existing schemas to add or change fields

## Additional Resources

- [Keystatic Documentation](https://keystatic.com/docs/introduction)
- [Astro Content Collections](https://docs.astro.build/en/guides/content-collections/)
- [Astro x Keystatic Tutorial](https://maciekpalmowski.dev/blog/keystatic-x-astro/)
