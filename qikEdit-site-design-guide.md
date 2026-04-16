# qikEdit Website Design Specification (Version 2.1.8)


This document provides a complete guide for building websites that are compatible with the qikEdit 2.1.7 visual CMS. By following this specification, you can create static websites that allow content editing through the qikEdit application.

  
## Table of Contents

  

1. [Overview](#overview)

2. [Basic Concepts](#basic-concepts)

3. [qik Tag Types](#qik-tag-types)

4. [Special Section Tags](#special-section-tags)

5. [qikForms Integration](#qikforms-integration)

6. [Best Practices](#best-practices)

7. [Example Implementations](#example-implementations)

  

---

  

## Overview

  

qikEdit allows static website owners to edit their content through a visual WYSIWYG interface. This is accomplished by adding special comment tags to your HTML, PHP, or JavaScript files that mark regions as editable.

  

### Key Benefits

  

- Keep the performance and security benefits of static websites

- Provide a user-friendly editing interface without a database

- Edit content by clicking directly on the rendered page

- Manage portfolios, galleries, and playlists with structured interfaces

- Connect via SFTP for direct file editing

  

### How It Works

  

1. Developers add qik tags to mark editable regions in their code

2. Users connect to their website via SFTP using qikEdit

3. The website renders in qikEdit's preview pane

4. Users click on tagged regions to edit them

5. Changes are published directly to the SFTP server

  

---

  

## Basic Concepts

  

### Tag Syntax

  

All qik tags follow this pattern:

```

[OPENING TAG] [field-name] [(optional description)]

[EDITABLE CONTENT]

[CLOSING TAG]

```

  

### Field Names



- **Allowed characters**: Letters (uppercase and lowercase), numbers, hyphens (`-`), and underscores (`_`)

- **Best practice**: Use lowercase with hyphens for readability (e.g., `hero-tagline`, `about-text`, `email-address`)

- **Display names**: Hyphens are converted to spaces and each word is title-cased automatically
  - Example: `hero-tagline` → "Hero Tagline"
  - Example: `email-address` → "Email Address"
  - Note: Underscores are preserved in display names (e.g., `my_field` → "My_field")

  

### Descriptions

  

- Optional but recommended

- Shown to the user in the editing interface

- Helps clarify what content belongs in the field

- Placed in parentheses after the field name

  

---

  

## qik Tag Types

qikEdit supports nine distinct tag types, each designed for specific content editing needs:

1. **Standard (WYSIWYG)** - Rich text editing with formatting controls
2. **Text-Only** - Plain text, URLs, and code without WYSIWYG formatting
3. **Image** - Swappable images via visual media picker
4. **Portfolio** - Structured collections of work samples and projects
5. **Gallery** - Photo gallery management with image uploads
6. **Playlist** - Audio playlist management
7. **Blog** - Blog post metadata and automatic listing generation
8. **Contact Forms (qik-form)** - Embedded qikForms contact forms (see qikForms Integration section)
9. **Navigation (qik-nav)** - Site navigation menu management with drag-and-drop reordering

**Comment Syntax Compatibility:** All tag types support three comment syntaxes:
- HTML comments (`<!-- -->`) for HTML and PHP files
- JavaScript single-line comments (`//`) for JavaScript files
- JavaScript multi-line comments (`/* */`) for JavaScript files

---

### 1. Standard WYSIWYG Tags



These fields support rich text editing with a visual editor (bold, italic, links, etc.).

  

#### HTML Comment Syntax

  

```html

<!-- qik field-name (Description of this field) -->

<p>This content can be edited with WYSIWYG tools.</p>

<p>Multiple paragraphs, <strong>formatting</strong>, and <a href="#">links</a> are supported.</p>

<!-- qik-end -->

```

  

**Use cases:**

- Hero section text

- About sections

- Article body content

- Any HTML content that benefits from formatting

  

**Example:**

```html

<!-- qik hero-tagline (Large header text, single line.) -->

<p class="tagline">Professional Voice Over Talent</p>

<!-- qik-end -->

  

<!-- qik about-text (Primary bio area, paragraph content.) -->

<h2>About Mike</h2>

<p>I'm an actor with over 10 years of experience who also has worked on voice projects for the same time. I am someone who loves to do the weird thing, the "out there" thing, and love adapting to new challenges.</p>

<p>Whether you need a commanding narrator, a friendly spokesperson, or something completely unconventional, I bring authenticity and creativity to every project.</p>

<!-- qik-end -->

```

  

#### JavaScript Single-Line Comment Syntax

  

```javascript

// qik field-name (Description of this field)

const value = 'editable content';

// qik-end

```

  

**Example:**

```javascript

// qik api-key (API key for external service)

const API_KEY = 'sk-1234567890abcdef';

// qik-end

```

  

#### JavaScript Multi-Line Comment Syntax

  

```javascript

/* qik field-name (Description of this field) */

const value = 'editable content';

/* qik-end */

```

  

**Example:**

```javascript

/* qik tracking-code (Google Analytics tracking code) */

gtag('config', 'G-JSCH67PDNK');

/* qik-end */

```

  

---



### 2. Text-Only Tags



These fields do NOT have WYSIWYG editing—they're for plain text, URLs, file paths, or code snippets.

  

#### HTML Comment Syntax

  

```html

<!-- qik-text field-name (Description of this field) -->

Plain text content only

<!-- qik-end -->

```

  

**Use cases:**

- URLs

- File paths

- Email addresses

- Phone numbers

- Short text snippets that shouldn't contain HTML

  

**Example:**

```html

<!-- qik-text email-address (Contact email address) -->

mike@mikedeevoiceover.com

<!-- qik-end -->

  

<!-- qik-text phone-number (Contact phone number) -->

(612) 547-9791

<!-- qik-end -->

  

<!-- qik-text reel-url (Audio file path for demo reel) -->

/media/commercial-demo.mp3

<!-- qik-end -->

```

  

#### JavaScript Single-Line Comment Syntax

  

```javascript

// qik-text field-name (Description of this field)

'plain text value'

// qik-end

```

  

**Example:**

```javascript

// qik-text audio-file-path (Path to audio file)

'/media/demo-reel.mp3'

// qik-end

```

  

#### JavaScript Multi-Line Comment Syntax

  

```javascript

/* qik-text field-name (Description of this field) */

'plain text value'

/* qik-end */

```

  

**Example:**

```javascript

const audioSources = {

/* qik-text reel1-url (Audio file path for first reel) */

1: '/media/commercial-demo.mp3',

/* qik-end */

  

/* qik-text reel2-url (Audio file path for second reel) */

2: '/media/radio-demo.mp3'

/* qik-end */

};

```

  

---

**Note on Lists:** Lists are simply standard WYSIWYG tags that contain `<ul>` or `<ol>` elements. Users can add items by pressing Enter in the editor.

```html
<!-- qik equipment-list (Bulleted list of studio equipment) -->
<ul>
<li>Sound-treated recording room</li>
<li>Rode NT1 Condenser Mic</li>
<li>Behringer MIC500USB Pre-Amp</li>
<li>Professional audio editing software</li>
</ul>
<!-- qik-end -->
```

---

### 3. Image Tags

Image tags allow users to swap individual images on the site via a visual media picker. When a user clicks an image wrapped in `qik-img` tags in the preview, an image selection modal opens showing available images from the `/media` folder, with the option to upload new images and edit alt text.

#### HTML Comment Syntax

```html
<!-- qik-img field-name (Description of this image) -->
<img src="/media/hero.jpg" alt="Hero image">
<!-- qik-end -->
```

**Use cases:**

- Hero/banner images
- Profile photos or team member headshots
- Logo images
- Any standalone image that the site owner should be able to swap without touching code

**Example:**

```html
<!-- qik-img hero-image (Main hero background image) -->
<img src="/media/hero.jpg" alt="Hero image">
<!-- qik-end -->

<!-- qik-img profile-photo (Team member headshot) -->
<img src="/media/profile.jpg" alt="Profile photo">
<!-- qik-end -->

<!-- qik-img logo (Site logo) -->
<img src="/media/logo.png" alt="Company logo">
<!-- qik-end -->
```

#### JavaScript Single-Line Comment Syntax

```javascript
// qik-img field-name (Description)
'<img src="/media/image.jpg" alt="Description">'
// qik-end
```

#### JavaScript Multi-Line Comment Syntax

```javascript
/* qik-img field-name (Description) */
'<img src="/media/image.jpg" alt="Description">'
/* qik-end */
```

#### How Image Tags Work

1. The `qik-img` tag wraps an `<img>` element
2. In the preview, hovering over the image shows a highlight overlay with the field name
3. Clicking the image opens an image selection modal (instead of a text editor)
4. The modal displays the current image, an alt text input, dimension controls (width/height with aspect ratio lock), and a grid of available images from `/media`
5. Users can select an existing image or upload a new one
6. Users can optionally set image dimensions (width and height in pixels). A lock button keeps the aspect ratio proportional — changing one dimension automatically adjusts the other. Leaving dimensions empty renders the image at its natural size
7. On save, the `<img>` tag's `src`, `alt`, and optional `width`/`height` attributes are updated
8. Publishing writes the updated `<img>` tag back to the file

**Dimensions example:**
```html
<!-- Without dimensions (natural size) -->
<img src="/media/hero.jpg" alt="Hero image">

<!-- With dimensions -->
<img src="/media/hero.jpg" alt="Hero image" width="800" height="600">
```

#### Field Name Rules

Same rules as standard qik tags:
- Allowed characters: letters, numbers, hyphens (`-`), underscores (`_`)
- Best practice: lowercase with hyphens (e.g., `hero-image`, `profile-photo`)
- Display names are automatically generated from field names (e.g., `hero-image` → "Hero Image")

---

## Special Section Tags

### 4. Portfolio Tags

  

Portfolio sections allow users to manage a collection of portfolio items (projects, case studies, work samples, etc.) with a structured interface.

  

#### HTML Syntax

  

```html

<!-- qik-portfolio -->

<section class="portfolio-section" id="portfolio">

<div class="portfolio-container">

<h2>Portfolio</h2>

<div class="portfolio-grid">

  

<div class="portfolio-item">

<img src="/media/project1.jpg" alt="Project 1" class="portfolio-image">

<div class="portfolio-content">

<h3>Project Title</h3>

<p class="client">Client Name</p>

<p>Project description goes here.</p>

<a href="https://example.com" target="_blank" class="portfolio-link">View Project</a>

</div>

</div>

  

<div class="portfolio-item">

<img src="/media/project2.jpg" alt="Project 2" class="portfolio-image">

<div class="portfolio-content">

<h3>Another Project</h3>

<p class="client">Another Client</p>

<p>Another project description.</p>

<a href="https://example.com" target="_blank" class="portfolio-link">View Project</a>

</div>

</div>

  

</div>

</div>

</section>

<!-- qik-portfolio-end -->

```

  

#### Required Structure



For portfolio items to be editable, each item must:



1. **Be a container element** with a class attribute that meets one of these requirements:

   - **Option A**: Class attribute contains BOTH the word `portfolio` AND the word `item` (anywhere in the class)
   - **Option B**: Class is exactly `portfolio-item`

   **Valid examples:**
   - ✅ `class="portfolio-item"` (contains both words)
   - ✅ `class="work-portfolio-item"` (contains both words)
   - ✅ `class="portfolio-card-item"` (contains both words)
   - ✅ `class="item portfolio"` (both words, different order)
   - ✅ `class="my-portfolio card-item"` (both words in different parts)

   **Invalid examples:**
   - ❌ `class="portfolio"` (missing "item")
   - ❌ `class="portfolio-card"` (missing "item")
   - ❌ `class="work-item"` (missing "portfolio")

  

2. **Contain specific elements** (all optional, but recommended):

   - **Title**: `<h3>`, `<h2>`, or `<h4>` element (first match is used)

   - **Client**: Element with class exactly `client` OR containing the text `client` anywhere in the class
     - Examples: `<p class="client">`, `<span class="project-client">`, `<div class="client-name">`

   - **Description**: Any `<p>` element that is NOT the client element

   - **Link**: First `<a>` element found (extracts href, text content, and target attribute)

   - **Image**: First `<img>` element found (extracts src attribute)

  

3. **The qikEdit interface will show fields for:**

- Title

- Client

- Description

- Image URL

- Link URL

- Link Text

- Link Target (new tab checkbox)

  

#### JavaScript Syntax

  

```javascript

// qik-portfolio

// Portfolio items go here

// qik-portfolio-end

```

  

Or:

  

```javascript

/* qik-portfolio */

/* Portfolio items go here */

/* qik-portfolio-end */

```

  

---



### 5. Gallery Tags



Gallery sections allow users to manage photo galleries with a visual interface for adding, removing, and reordering photos.

  

#### HTML Syntax

  

```html

<!-- qik-gallery -->

<section class="gallery-section">

<div class="gallery-grid">

  

<div class="photo-item">

<img src="/media/photo1.jpg" alt="Photo 1">

</div>

  

<div class="photo-item">

<img src="/media/photo2.jpg" alt="Photo 2">

</div>

  

<div class="photo-item">

<img src="/media/photo3.jpg" alt="Photo 3">

</div>

  

</div>

</section>

<!-- qik-gallery-end -->

```

  

#### Required Structure



For gallery items to be editable, each item must:



1. **Be a container element** with a class attribute that:

   - Is exactly `photo-item`, OR
   - Contains the text `photo-item` anywhere in the class attribute

   **Valid examples:**
   - ✅ `class="photo-item"`
   - ✅ `class="gallery-photo-item"`
   - ✅ `class="photo-item-wrapper"`
   - ✅ `class="main-photo-item-card"`

  

2. **Contain an `<img>` element** with:

- `src` attribute (the image URL)

- `alt` attribute (the image description)

  

#### JavaScript Syntax

  

```javascript

// qik-gallery

// Gallery items go here

// qik-gallery-end

```

  

Or:

  

```javascript

/* qik-gallery */

/* Gallery items go here */

/* qik-gallery-end */

```

  

---



### 6. Playlist Tags



Playlist sections allow users to manage audio playlists with a structured interface for adding, removing, and reordering tracks.

  

#### HTML Syntax

  

```html

<!-- qik-playlist demo-reels -->

<div class="playlist-container">

  

<div class="playlist-item" data-audio="/media/commercial-demo.mp3">

<div class="playlist-title">Commercial Demo Reel</div>

</div>

  

<div class="playlist-item" data-audio="/media/radio-demo.mp3">

<div class="playlist-title">Radio Spot Reel</div>

</div>

  

<div class="playlist-item" data-audio="/media/halloween-demo.mp3">

<div class="playlist-title">Halloween Reel</div>

</div>

  

</div>

<!-- qik-playlist-end demo-reels -->

```

  

**Note:** Playlists require a **name** that must match in both opening and closing tags.

  

#### Required Structure



For playlist items to be editable, each item must:



1. **Be a container element** with a class attribute that:

   - Is exactly `playlist-item`, OR
   - Contains the text `playlist-item` anywhere in the class attribute

   **Valid examples:**
   - ✅ `class="playlist-item"`
   - ✅ `class="audio-playlist-item"`
   - ✅ `class="playlist-item-wrapper"`
   - ✅ `class="main-playlist-item-card"`

  

2. **Have a `data-audio` attribute** containing the path to the audio file

  

3. **Contain a title element** with a class attribute that:

   - Is exactly `playlist-title`, OR
   - Contains the text `playlist-title` anywhere in the class attribute

   **Valid examples:**
   - ✅ `class="playlist-title"`
   - ✅ `class="track-playlist-title"`
   - ✅ `class="playlist-title-text"`

  

#### JavaScript Syntax

  

```javascript

// qik-playlist playlist-name

// Playlist items go here

// qik-playlist-end playlist-name

```

  

Or:

  

```javascript

/* qik-playlist playlist-name */

/* Playlist items go here */

/* qik-playlist-end playlist-name */

```

---

### 7. Blog Tags (qikBlog)

qikBlog is a blog management feature that enables users to create, manage, and organize blog posts on their static qik-enabled websites. Blog posts are standard HTML files with qik tags, stored in a `/blog/` subdirectory, and automatically listed on a `blog.html` page.

#### Blog Detection

qikBlog features are automatically enabled when a `blog.html` file exists in your website root directory. The Blog Manager will appear in the navigation once qikEdit detects this file.

#### Blog Post Metadata Tag

Each blog post must include a `qik-blog-meta` tag in the `<head>` section containing JSON metadata:

```html
<!-- qik-blog-meta
{
  "title": "My Blog Post Title",
  "date": "2026-01-15",
  "featuredImage": "/media/featured.jpg",
  "hidden": false,
  "tagline": "A brief description for SEO purposes"
}
qik-blog-meta-end -->
```

**Metadata Fields:**
- **title** (required): The blog post title, used in listings and page title
- **date** (required): Publication date in ISO format (YYYY-MM-DD)
- **featuredImage** (optional): Path to featured image, displayed in blog listings
- **hidden** (optional): If `true`, post won't appear in blog.html but remains accessible via direct URL
- **tagline** (optional): SEO description, used in meta description tag

#### Blog Listing Tag

The `blog.html` file must include a `qik-blog-list` section where qikEdit will automatically generate the blog post listings:

```html
<div class="blog-posts-container">
  <!-- qik-blog-list -->
  <!-- AUTO-GENERATED: This section is managed by qikEdit -->
  <!-- qik-blog-list-end -->
</div>
```

When you create, update, or delete blog posts, qikEdit automatically regenerates this section with all visible (non-hidden) posts, sorted by date (newest first).

**Generated HTML Structure:**

```html
<!-- qik-blog-list -->
  <article class="blog-post-preview">
    <a href="blog/my-post.html">
      <img src="/media/image.jpg" alt="Post Title" class="post-featured-image">
      <h2>Post Title</h2>
      <time datetime="2026-01-15">January 15, 2026</time>
    </a>
  </article>
  <article class="blog-post-preview">
    <a href="blog/another-post.html">
      <h2>Another Post</h2>
      <time datetime="2026-01-10">January 10, 2026</time>
    </a>
  </article>
<!-- qik-blog-list-end -->
```

#### Sample blog.html Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><!-- qik page-title -->Blog<!-- qik-end --></title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <!-- qik header-content (Site header area) -->
    <nav>
      <a href="index.html">Home</a>
      <a href="blog.html">Blog</a>
    </nav>
    <!-- qik-end -->
  </header>

  <main>
    <h1><!-- qik blog-heading -->Our Blog<!-- qik-end --></h1>

    <p><!-- qik blog-intro (Blog introduction text) -->
    Welcome to our blog. Here you'll find our latest posts and updates.
    <!-- qik-end --></p>

    <div class="blog-posts-container">
      <!-- qik-blog-list -->
      <!-- AUTO-GENERATED: This section is managed by qikEdit -->
      <!-- qik-blog-list-end -->
    </div>
  </main>

  <footer>
    <!-- qik footer-content (Site footer area) -->
    <p>&copy; 2026 Your Website</p>
    <!-- qik-end -->
  </footer>
</body>
</html>
```

#### Sample Blog Post Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- qik-blog-meta
  {
    "title": "Sample Blog Post",
    "date": "2026-01-15",
    "featuredImage": "/media/sample.jpg",
    "hidden": false,
    "tagline": "This is a sample blog post for demonstration"
  }
  qik-blog-meta-end -->

  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sample Blog Post</title>
  <meta name="description" content="This is a sample blog post for demonstration">
  <link rel="stylesheet" href="../styles.css">
</head>
<body>
  <header>
    <!-- qik header-content (Site header area) -->
    <nav>
      <a href="../index.html">Home</a>
      <a href="../blog.html">Blog</a>
    </nav>
    <!-- qik-end -->
  </header>

  <main class="blog-post">
    <article>
      <h1><!-- qik post-title -->Sample Blog Post<!-- qik-end --></h1>

      <div class="post-content">
        <!-- qik post-body (Main blog post content) -->
        <p>This is the main content of your blog post. Edit this section to add your content.</p>
        <p>You can include images, links, and any HTML formatting.</p>
        <!-- qik-end -->
      </div>
    </article>
  </main>

  <footer>
    <!-- qik footer-content (Site footer area) -->
    <p>&copy; 2026 Your Website</p>
    <!-- qik-end -->
  </footer>
</body>
</html>
```

#### Best Practices for qikBlog

**File Organization:**
- Keep all blog post HTML files in the `/blog/` directory
- Use descriptive, URL-friendly filenames (e.g., `my-first-post.html`, `introducing-new-features.html`)
- Store blog-related images in `/media/` or `/blog/media/` for organization

**Metadata Guidelines:**
- Always include title and date in the `qik-blog-meta` tag
- Use ISO date format (YYYY-MM-DD) for consistent sorting
- Add meaningful taglines for better SEO
- Use the `hidden` field to work on draft posts before publishing

**Content Structure:**
- Use standard qik tags within blog posts for editable content
- Keep a consistent template across all blog posts for uniform styling
- Include navigation back to `blog.html` and your main site

**Creating Your First Post:**
1. Create `blog.html` in your website root with the `qik-blog-list` tags
2. Manually create your first blog post HTML file in `/blog/` directory
3. Include the `qik-blog-meta` tag with all required fields
4. Once you have one post, use qikEdit's "New Post" feature to create additional posts from the template

**Managing Posts:**
- Use the Blog Manager in qikEdit to view all posts
- Click "Settings" to update metadata without editing the full post
- Use "Hidden" to hide posts from the listing while keeping them accessible
- Duplicate existing posts to maintain consistent structure
- qikEdit automatically updates `blog.html` when you create, update, or delete posts

---

## qikForms Integration

### 8. Contact Form Tags (qik-form)

qikForms is an integrated contact form management system that allows you to embed forms created through the qikEdit form builder directly into your qik-enabled websites. Forms created in qikEdit are automatically configured with spam protection, rate limiting, and submission handling.

#### How qikForms Works

1. **Create a form** using the qikForms builder in qikEdit (available when logged in via qikSites)
2. **Configure form fields** (name, email, phone, message, etc.) with validation rules
3. **Generate embed code** from the form builder
4. **Wrap the embed code** with `qik-form` tags in your HTML
5. **Edit forms visually** in qikEdit without touching code

#### Contact Form Tag Structure

Contact form tags wrap the qikForms embed script to make them identifiable and manageable within qikEdit.

**HTML Syntax:**
```html
<!-- qik-form -->
<script
  src="https://platform.qiksites.io/qikforms/embed.js"
  data-qikadmin-form-id="123"
  async>
</script>
<!-- qik-form-end -->
```

**JavaScript Single-Line Syntax:**
```javascript
// qik-form
const formScript = document.createElement('script');
formScript.src = 'https://platform.qiksites.io/qikforms/embed.js';
formScript.setAttribute('data-qikadmin-form-id', '123');
document.body.appendChild(formScript);
// qik-form-end
```

**JavaScript Multi-Line Syntax:**
```javascript
/* qik-form */
const formScript = document.createElement('script');
formScript.src = 'https://platform.qiksites.io/qikforms/embed.js';
formScript.setAttribute('data-qikadmin-form-id', '123');
document.body.appendChild(formScript);
/* qik-form-end */
```

#### Required Structure

For form tags to be properly detected and editable:

1. **The script tag must include** `data-qikadmin-form-id` attribute with the form ID
2. **The script source** should point to the qikForms embed script
3. **Wrap with qik-form tags** for visual identification in qikEdit

#### Best Practices for qikForms

**Form Creation:**
- Create forms in qikEdit's form builder before embedding (requires qikSites login)
- Configure all fields, validation, and settings before generating embed code
- Use descriptive form names to easily identify them later

**Embedding Forms:**
- Wrap the generated embed code with `qik-form` / `qik-form-end` tags
- Place forms in logical locations on your site (contact page, footer, etc.)
- The form will automatically render at the script tag location

**Form Management:**
- Forms can be edited through qikEdit's visual interface
- Changes to form configuration update automatically without code changes
- View submissions through the qikSites platform dashboard

**Security Features:**
- Forms include automatic spam protection
- Rate limiting prevents abuse
- Domain restrictions ensure forms only work on authorized domains
- Optional reCAPTCHA integration for additional protection

#### Example Implementation

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Us</title>
</head>
<body>
  <main>
    <h1>Contact Us</h1>
    <p>Have questions? Send us a message using the form below.</p>

    <!-- qik-form -->
    <script
      src="https://platform.qiksites.io/qikforms/embed.js"
      data-qikadmin-form-id="42"
      async>
    </script>
    <!-- qik-form-end -->
  </main>
</body>
</html>
```

**Note:** qikForms functionality requires a qikSites account and is only available when logged in through the qikSites platform integration in qikEdit.

---

### 9. Navigation Tags (qik-nav)

Navigation tags enable visual management of website navigation menus through qikEdit's interface. Users can add, edit, delete, and reorder navigation links with drag-and-drop functionality, and changes automatically sync across all files containing the same navigation.

#### How Navigation Tags Work

1. **Wrap your navigation** with `qik-nav` tags and give it a unique name
2. **Click the navigation** in qikEdit's preview to open the navigation editor
3. **Manage links** using a visual interface with drag-and-drop reordering
4. **Multi-file sync** automatically updates the navigation across all site files

#### Navigation Tag Structure

Navigation tags wrap the navigation menu container (typically a `<ul>` element) and require a unique name to support multiple navigations per page.

**HTML Syntax:**
```html
<!-- qik-nav main-nav -->
<ul>
  <li><a href="index.html">Home</a></li>
  <li><a href="about.html">About</a></li>
  <li><a href="portfolio.html">Portfolio</a></li>
  <li><a href="contact.html">Contact</a></li>
</ul>
<!-- qik-nav-end main-nav -->
```

**JavaScript Single-Line Syntax:**
```javascript
// qik-nav main-nav
const navItems = [
  { text: 'Home', url: 'index.html' },
  { text: 'About', url: 'about.html' }
];
// qik-nav-end main-nav
```

**JavaScript Multi-Line Syntax:**
```javascript
/* qik-nav main-nav */
const navItems = [
  { text: 'Home', url: 'index.html' },
  { text: 'About', url: 'about.html' }
];
/* qik-nav-end main-nav */
```

#### Named Navigation Menus

Navigation tags require a unique name to:
- Support multiple navigations per page (header nav, footer nav, mobile nav)
- Enable multi-file synchronization across the site
- Identify which navigation to edit when clicked

**Example with multiple navigations:**
```html
<!-- Header Navigation -->
<!-- qik-nav header-nav -->
<ul class="main-menu">
  <li><a href="index.html">Home</a></li>
  <li><a href="about.html">About</a></li>
  <li><a href="contact.html">Contact</a></li>
</ul>
<!-- qik-nav-end header-nav -->

<!-- Footer Navigation -->
<!-- qik-nav footer-nav -->
<ul class="footer-menu">
  <li><a href="privacy.html">Privacy</a></li>
  <li><a href="terms.html">Terms</a></li>
</ul>
<!-- qik-nav-end footer-nav -->
```

#### Supported Navigation Structures

qikEdit's navigation manager intelligently detects and supports three common navigation patterns:

**1. Standard Navigation (ul > li > a)**
```html
<!-- qik-nav main-nav -->
<ul>
  <li><a href="index.html">Home</a></li>
  <li><a href="about.html">About</a></li>
  <li><a href="services.html">Services</a></li>
</ul>
<!-- qik-nav-end main-nav -->
```

**2. Bootstrap Navigation (.nav-item and .nav-link classes)**
```html
<!-- qik-nav main-nav -->
<ul class="nav">
  <li class="nav-item">
    <a class="nav-link" href="index.html">Home</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" href="about.html">About</a>
  </li>
</ul>
<!-- qik-nav-end main-nav -->
```

**3. Custom Structures**
The navigation manager automatically adapts to your HTML structure, preserving CSS classes and element types when rebuilding navigation after edits.

#### Navigation Editor Features

When you click a navigation in qikEdit's preview, the navigation editor provides:

**Add Links:**
- Click "+ Add Navigation Link" button
- Enter link text and URL
- Optional "Open in new tab" checkbox
- Supports both relative URLs (`about.html`) and absolute URLs (`https://example.com`)

**Edit Links:**
- Click the pencil icon on any navigation item
- Update link text or URL
- Toggle new tab setting

**Delete Links:**
- Click the trash icon on any item
- Confirmation prompt prevents accidental deletion

**Reorder Links:**
- **Drag-and-drop**: Grab the six-dot handle and drag items to reorder
- **Up/Down buttons**: Click arrow buttons to move items one position at a time
- Changes save automatically and update across all files

**Preserved Data:**
- Original CSS classes on list items (`<li>`) are preserved
- Original CSS classes on links (`<a>`) are preserved
- HTML structure and formatting are maintained

#### Multi-File Synchronization

When you save navigation changes, qikEdit automatically:

1. **Recursively scans your entire site** for all HTML and PHP files
   - Searches through all directories in your web root
   - Finds every `.html`, `.htm`, and `.php` file
   - No file naming restrictions - works with any filename

2. **Detects matching navigation tags** by comparing navigation names
   - Checks each file for the specific `qik-nav` tag you edited
   - Only updates files that contain the matching navigation

3. **Updates all instances** simultaneously
   - Preserves CSS classes and HTML structure
   - Strips dynamic "active" classes to prevent conflicts
   - Maintains comment style consistency

4. **Shows progress and confirmation**
   - Progress modal displays files being checked and updated
   - Final message: "Navigation updated in X files"
   - Console logging available for debugging

**Best Practice:** This ensures consistent navigation across your entire site without manual updates, even with custom page names or complex directory structures.

#### Integration with Page Duplication

When duplicating a page in qikEdit, you can automatically add it to navigation:

1. **Checkbox appears** if qikEdit detects navigation tags in your site
2. **Select the navigation** menu from dropdown (shows all detected navigations)
3. **Choose position**:
   - End of menu (default)
   - Start of menu
   - After Home
4. **Automatic addition** - the new page link is added to all files containing that navigation

#### Active Page Highlighting

qikEdit automatically highlights the current page in navigation during preview:

**How It Works:**
- Detects which file you're currently editing
- Compares navigation link URLs to the current filename
- Adds `qik-active-page` class to matching links and their parent `<li>` elements
- Removes any existing "active" classes to prevent conflicts

**Styling:**
The active page indicator uses:
- Bold text weight
- qikEdit brand color (#8b6f47)
- Subtle underline effect

**Supported URL Formats:**
- Relative URLs: `about.html`, `pages/contact.html`
- Filename-only: `portfolio.html`
- Query strings and anchors are ignored for matching

**Important Notes:**
- Highlighting is **preview-only** and not saved to HTML files
- This prevents hardcoded "active" classes that break on other pages
- Your existing CSS for "active" states will work normally on the live site
- qikEdit strips dynamic active classes when rebuilding navigation to maintain clean HTML

**Customizing Active Styles:**
To style the active page indicator, add CSS to your site:
```css
.qik-active-page {
  font-weight: bold;
  color: #your-brand-color;
  border-bottom: 2px solid #your-brand-color;
}
```

#### Required Structure

For navigation tags to work properly:

1. **Navigation container** must be a `<ul>`, `<nav>`, or `<div>` element
2. **Navigation items** should be `<li>` elements (or match your existing structure)
3. **Links** must be `<a>` elements with `href` attributes
4. **Named tags** - both opening and closing tags must include the same navigation name

#### Best Practices for Navigation Tags

**Naming Convention:**
- Use descriptive names: `main-nav`, `header-nav`, `footer-nav`, `mobile-nav`
- Names should be lowercase with hyphens for consistency
- Names must match in opening and closing tags

**Structure Guidelines:**
- Wrap only the menu container (e.g., `<ul>`), not outer sections or headers
- Keep navigation HTML as simple as possible
- Use CSS classes for styling, not inline styles (preserved during edits)
- Avoid hardcoded "active" classes - qikEdit automatically highlights the current page

**CSS Class Management:**
- All CSS classes on `<li>` and `<a>` elements are preserved during edits
- Dynamic "active" classes (active, current, selected) are automatically stripped to prevent conflicts
- qikEdit adds `qik-active-page` class in preview to highlight the current page
- Original styling and custom classes remain untouched

**Multi-Navigation Sites:**
- Give each navigation a unique name
- Header and footer navigations can share the same name if they should stay synchronized
- Mobile and desktop menus should use different names if they have different items

**File Organization:**
- If using PHP includes for navigation, wrap the include file content with `qik-nav` tags
- For shared navigation across pages, place it in a reusable component file
- Works with any directory structure or file naming convention

#### Example Implementations

**Complete Header with Navigation:**
```html
<header>
  <div class="header-container">
    <div class="logo">
      <a href="index.html">
        <img src="/media/logo.png" alt="<!-- qik-text site-name -->My Website<!-- qik-end -->">
      </a>
    </div>

    <nav class="main-navigation">
      <!-- qik-nav main-nav -->
      <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="portfolio.html">Portfolio</a></li>
        <li><a href="blog.html">Blog</a></li>
        <li><a href="contact.html">Contact</a></li>
      </ul>
      <!-- qik-nav-end main-nav -->
    </nav>
  </div>
</header>
```

**Bootstrap Navigation Example:**
```html
<nav class="navbar navbar-expand-lg">
  <div class="container">
    <!-- qik-nav header-nav -->
    <ul class="navbar-nav">
      <li class="nav-item">
        <a class="nav-link active" href="index.html">Home</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="services.html">Services</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="contact.html">Contact</a>
      </li>
    </ul>
    <!-- qik-nav-end header-nav -->
  </div>
</nav>
```

**Footer Navigation Example:**
```html
<footer>
  <div class="footer-content">
    <div class="footer-navigation">
      <!-- qik-nav footer-nav -->
      <ul class="footer-links">
        <li><a href="privacy.html">Privacy Policy</a></li>
        <li><a href="terms.html">Terms of Service</a></li>
        <li><a href="sitemap.html">Sitemap</a></li>
      </ul>
      <!-- qik-nav-end footer-nav -->
    </div>

    <!-- qik footer-copyright -->
    <p>&copy; 2026 Your Company. All rights reserved.</p>
    <!-- qik-end -->
  </div>
</footer>
```

**PHP Include File Navigation:**
```php
<!-- File: includes/navigation.php -->
<!-- qik-nav main-nav -->
<ul class="menu">
  <li><a href="/index.html">Home</a></li>
  <li><a href="/about.html">About</a></li>
  <li><a href="/services.html">Services</a></li>
  <li><a href="/contact.html">Contact</a></li>
</ul>
<!-- qik-nav-end main-nav -->
```

#### Navigation Features Summary

**Supported:**
- ✅ Add, edit, delete navigation links
- ✅ Drag-and-drop reordering
- ✅ Move up/down buttons
- ✅ External links with "open in new tab" option
- ✅ Relative and absolute URLs
- ✅ Multiple navigations per page
- ✅ Multi-file synchronization across entire site
- ✅ Recursive site scanning (works with any filename)
- ✅ CSS class preservation
- ✅ Standard, Bootstrap, and custom HTML structures
- ✅ Automatic integration with page duplication
- ✅ Active page highlighting in preview (auto-detects current file)
- ✅ Progress indicators during multi-file updates

**Not Currently Supported (Future Enhancement):**
- ❌ Nested/dropdown menus (planned for future release)

#### Troubleshooting Navigation Tags

**Navigation not appearing in preview:**
- Verify both opening and closing tags have matching names
- Check that tags wrap a valid container element (`<ul>`, `<nav>`, or `<div>`)
- Ensure links are inside `<a>` elements with `href` attributes
- Refresh the preview if navigation was recently added

**Changes not saving across all files:**
- Check browser console for debug messages: `[Navigation] Multi-file sync complete: X files updated`
- Verify files contain the exact same navigation name in their `qik-nav` tags
- Ensure proper SFTP write permissions on all files
- Check that files are valid HTML/PHP (scanner only processes `.html`, `.htm`, `.php`)

**Active page not highlighting correctly:**
- qikEdit matches navigation links to the current filename
- Link `href` must match the filename (e.g., `about.html` matches `about.html`)
- Works with relative paths - absolute paths or anchors won't match
- Highlighting is visual-only in preview, not saved to HTML

**Original styling lost after editing:**
- This shouldn't happen - CSS classes are preserved during edits
- If it occurs, check that classes are on the `<li>` and `<a>` elements, not wrapper divs
- Note: Dynamic "active" classes are automatically stripped to prevent conflicts
- Report as a bug if non-active styling is consistently lost

**Multi-file sync slow or timing out:**
- Normal for large sites (100+ pages)
- Progress modal shows real-time status
- Check console for specific file errors
- Ensure stable SFTP connection

---

## Using qik Tags in JavaScript Files

All qik tag types (Standard, Text-Only, Image, Portfolio, Gallery, Playlist, and Contact Forms) can be used within JavaScript files or `<script>` tags using JavaScript comment syntax.

#### Single-Line Comment Syntax

```javascript
// qik field-name (Description)
const value = 'editable content';
// qik-end

// qik-text field-name (Description)
'plain text value'
// qik-end

// qik-img field-name (Description)
'<img src="/media/image.jpg" alt="Description">'
// qik-end

// qik-portfolio
// Portfolio items
// qik-portfolio-end

// qik-gallery
// Gallery items
// qik-gallery-end

// qik-playlist playlist-name
// Playlist items
// qik-playlist-end playlist-name

// qik-form
const formScript = document.createElement('script');
formScript.src = 'https://platform.qiksites.io/qikforms/embed.js';
formScript.setAttribute('data-qikadmin-form-id', '123');
// qik-form-end
```

#### Multi-Line Comment Syntax

```javascript
/* qik field-name (Description) */
const value = 'editable content';
/* qik-end */

/* qik-text field-name (Description) */
'plain text value'
/* qik-end */

/* qik-img field-name (Description) */
'<img src="/media/image.jpg" alt="Description">'
/* qik-end */

/* qik-portfolio */
/* Portfolio items */
/* qik-portfolio-end */

/* qik-gallery */
/* Gallery items */
/* qik-gallery-end */

/* qik-playlist playlist-name */
/* Playlist items */
/* qik-playlist-end playlist-name */

/* qik-form */
const formScript = document.createElement('script');
formScript.src = 'https://platform.qiksites.io/qikforms/embed.js';
formScript.setAttribute('data-qikadmin-form-id', '123');
/* qik-form-end */
```

**Use cases:**
- Configuration values in JavaScript files
- API keys and endpoints
- File paths and URLs in JavaScript arrays/objects
- Dynamic content loaded via JavaScript

**Example:**
```javascript
const config = {
  /* qik-text api-endpoint (API endpoint URL) */
  apiUrl: 'https://api.example.com/v1',
  /* qik-end */

  /* qik-text analytics-id (Google Analytics tracking ID) */
  gaTrackingId: 'G-JSCH67PDNK'
  /* qik-end */
};
```

---



## Best Practices

  

### 1. Use Descriptive Names and Descriptions

  

**Good:**

```html

<!-- qik hero-tagline (Large header text for the hero section, single line.) -->

<p class="tagline">Professional Voice Over Talent</p>

<!-- qik-end -->

```

  

**Bad:**

```html

<!-- qik text1 -->

<p class="tagline">Professional Voice Over Talent</p>

<!-- qik-end -->

```

  

### 2. Choose the Right Tag Type



- Use **qik** (WYSIWYG) for: Content with formatting, paragraphs, lists

- Use **qik-text** for: URLs, file paths, email addresses, phone numbers, plain text

- Use **qik-img** for: Standalone swappable images (hero images, profile photos, logos)

- Use **qik-portfolio** for: Collections of work samples or projects

- Use **qik-gallery** for: Photo galleries

- Use **qik-playlist** for: Audio playlists

- Use **qik-blog-meta** for: Blog post metadata and automated blog listings

- Use **qik-form** for: Embedded contact forms from qikForms builder

- Use **qik-nav** for: Site navigation menus with drag-and-drop management



### 3. Minimize HTML Elements Within Tags

**Important principle:** Include as few HTML elements as possible within qik tags—only include elements that need to be editable.

**Good (minimal elements):**
```html
<!-- qik hero-heading (Main hero heading) -->
<h1>Mike Dee</h1>
<!-- qik-end -->
```

**Bad (unnecessary wrapper):**
```html
<!-- qik hero-heading (Main hero heading) -->
<div class="heading-wrapper">
  <h1>Mike Dee</h1>
</div>
<!-- qik-end -->
```

**Good (text-only for URL):**
```html
<a href="<!-- qik-text email-address (Email address) -->mike@example.com<!-- qik-end -->">
  Email Me
</a>
```

**Bad (entire anchor tag wrapped):**
```html
<!-- qik email-link (Email link) -->
<a href="mailto:mike@example.com">Email Me</a>
<!-- qik-end -->
```

**Why this matters:**
- Cleaner code and easier maintenance
- Users only edit the content that should change
- Prevents accidental modification of structural HTML
- Keeps styling and structure separate from content

### 4. Keep Field Content Focused

  

Each field should represent one logical piece of content.



**Good (separate, focused fields):**
```html
<a href="mailto:<!-- qik-text contact-email (Contact email address) -->mike@example.com<!-- qik-end -->">
  Email Me
</a>

<a href="tel:<!-- qik-text contact-phone (Contact phone number, no formatting) -->6125479791<!-- qik-end -->">
  <!-- qik-text contact-phone-display (Phone number with formatting) -->(612) 547-9791<!-- qik-end -->
</a>

<!-- qik-text street-address (Street address) -->
123 Main St, City, State 12345
<!-- qik-end -->
```



**Bad (too much bundled together):**
```html
<!-- qik contact-info (All contact information) -->
<div>
<a href="mailto:mike@example.com">mike@example.com</a>
<a href="tel:6125479791">(612) 547-9791</a>
<p>123 Main St, City, State 12345</p>
</div>
<!-- qik-end -->
```



### 5. Use Consistent Naming Conventions



Pick a naming pattern and stick to it:

- `section-field` (e.g., `hero-tagline`, `about-text`, `footer-copyright`)

- `type-field` (e.g., `email-address`, `phone-number`, `image-url`)



### 6. Structure Special Sections Properly



For portfolio, gallery, and playlist sections to work correctly:

- Use the required class names

- Include all expected child elements

- Keep the HTML structure clean and consistent



### 7. Test in qikEdit



After adding qik tags:

1. Connect to your site via qikEdit

2. Verify all fields appear in the editor

3. Test editing and publishing changes

4. Check that the "All Fields" view shows hidden fields correctly



### 8. Consider Mobile Responsiveness

  

Remember that users can toggle between desktop and mobile views in qikEdit. Ensure your editable content looks good in both views.

  

---

  

## Example Implementations

  

### Complete Hero Section

  

```html

<section class="hero" id="home">

<div class="hero-content">

<!-- qik hero-heading (Main hero heading) -->

<h1>Mike Dee</h1>

<!-- qik-end -->

  

<!-- qik hero-tagline (Large header text, single line.) -->

<p class="tagline">Professional Voice Over Talent</p>

<!-- qik-end -->

  

<!-- qik hero-subtitle (Smaller text under the main header, single line.) -->

<p>Bringing scripts to life with versatility and passion</p>

<!-- qik-end -->

</div>

</section>

```

  

### Complete Contact Section

  

```html

<section class="contact-section" id="contact">

<div class="contact-container">

<!-- qik contact-heading (Contact section heading) -->

<h2>Let's Work Together</h2>

<!-- qik-end -->

  

<!-- qik contact-subtitle (Contact section subtitle) -->

<p class="contact-subtitle">Ready to bring your project to life? Get in touch today!</p>

<!-- qik-end -->

  

<div class="contact-info">

<div class="contact-item">
<span class="contact-icon">📧</span>
<div class="contact-details">
<h3>Email Me</h3>
<a href="mailto:<!-- qik-text contact-email (Contact email address) -->mike@mikedeevoiceover.com<!-- qik-end -->">
<!-- qik-text contact-email-display (Email address display text) -->mike@mikedeevoiceover.com<!-- qik-end -->
</a>
</div>
</div>

<div class="contact-item">
<span class="contact-icon">📱</span>
<div class="contact-details">
<h3>Call Me</h3>
<a href="tel:<!-- qik-text contact-phone-tel (Phone number for tel: link, no spaces or special characters) -->6125479791<!-- qik-end -->">
<!-- qik-text contact-phone-display (Phone number display text) -->(612) 547-9791<!-- qik-end -->
</a>
</div>
</div>

</div>

</div>

</section>

```

  

### Complete Portfolio Section

  

```html

<!-- qik-portfolio -->

<section class="portfolio-section" id="portfolio">

<div class="portfolio-container">

<h2>Portfolio</h2>

<div class="portfolio-grid">

  

<div class="portfolio-item">

<img src="/media/darkpony.jpg" alt="Dark Pony Radio" class="portfolio-image">

<div class="portfolio-content">

<h3>Character Work</h3>

<p class="client">Dark Pony Radio</p>

<p>Bringing diverse characters to life with authentic voices and compelling performances in audio drama productions.</p>

<a href="https://open.spotify.com/show/50SaySABtmIA317gnsSxnG" target="_blank" class="portfolio-link">Listen on Spotify</a>

</div>

</div>

  

<div class="portfolio-item">

<img src="/media/filmschoolslacker.jpg" alt="Film School Slacker" class="portfolio-image">

<div class="portfolio-content">

<h3>Podcast Voiceover</h3>

<p class="client">Film School Slacker</p>

<p>Professional narration for engaging podcast content with natural delivery and pacing.</p>

<a href="https://filmschoolslacker.com/" target="_blank" class="portfolio-link">Visit Website</a>

</div>

</div>

  

</div>

</div>

</section>

<!-- qik-portfolio-end -->

```

  

### Complete Footer with Social Links



```html
<footer>
<div class="social-links">
<a href="<!-- qik-text imdb-link (URL for IMDB profile) -->https://www.imdb.com/name/nm16461651<!-- qik-end -->" target="_blank" rel="noopener noreferrer" aria-label="IMDB Profile">
<i class="fab fa-imdb"></i>
</a>

<a href="<!-- qik-text instagram-link (URL for Instagram profile) -->https://www.instagram.com/mikedeevo<!-- qik-end -->" target="_blank" rel="noopener noreferrer" aria-label="Instagram Profile">
<i class="fab fa-instagram"></i>
</a>
</div>

<!-- qik footer-text (Footer copyright text) -->
<p>© 2025 Mike Dee Voiceover. All rights reserved.</p>
<!-- qik-end -->
</footer>
```

  

### JavaScript Configuration with qik Tags

  

```html

<script>

const audioSources = {

// qik-text reel1-url (Audio file path for commercial reel)

1: '/media/commercial-demo.mp3',

// qik-end

  

// qik-text reel2-url (Audio file path for radio reel)

2: '/media/radio-demo.mp3',

// qik-end

  

// qik-text reel3-url (Audio file path for halloween reel)

3: '/media/halloween-demo.mp3'

// qik-end

};

</script>

```



### Contact Form with qikForms



```html

<section class="contact-section" id="contact">

<div class="contact-container">

<h2>Get In Touch</h2>

<p>Fill out the form below and we'll get back to you as soon as possible.</p>



<!-- qik-form -->

<script

  src="https://platform.qiksites.io/qikforms/embed.js"

  data-qikadmin-form-id="42"

  async>

</script>

<!-- qik-form-end -->



</div>

</section>

```

**Note:** The form must be created in qikEdit's form builder first. The `data-qikadmin-form-id` value comes from the form builder after creating your form.



---



## Summary



By following this specification, you can create static websites that are fully editable through qikEdit's visual interface. The key points are:



1. **Use the right tag type** for your content:
   - **Standard (qik)** - WYSIWYG editing for formatted content
   - **Text-Only (qik-text)** - Plain text, URLs, and values without formatting
   - **Portfolio (qik-portfolio)** - Work samples and project collections
   - **Gallery (qik-gallery)** - Photo galleries
   - **Playlist (qik-playlist)** - Audio playlists
   - **Blog (qik-blog-meta)** - Blog post metadata and automated listings
   - **Contact Forms (qik-form)** - Embedded qikForms contact forms
   - **Navigation (qik-nav)** - Site navigation menu management with multi-file sync
   - All tag types work in HTML, PHP, and JavaScript files using appropriate comment syntax

2. **Minimize HTML within tags** - Only include elements that need to be editable

3. **Mark editable content** with qik tags using HTML or JavaScript comment syntax

4. **Follow naming conventions** and provide helpful descriptions

5. **Structure special sections properly** with required class names and elements

6. **Test your implementation** in qikEdit to ensure everything works as expected



This approach gives you the best of both worlds: the speed and security of static websites with the convenience of a visual CMS.