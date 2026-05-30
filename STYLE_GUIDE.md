# Style Guide — Tissue Culture Website

This document defines the design system for the Tissue Culture website. Every new page and section must follow these conventions. The CSS is driven by CSS custom properties defined in `assets/css/main.css` — do not override them with inline styles or hardcoded colors unless absolutely necessary.

---

## 1. Color System

All colors are controlled by CSS variables in `:root` (`main.css:9-17`). Never hardcode color values in HTML or custom CSS.

| Variable | Value | Role |
|----------|-------|------|
| `--background-color` | `#ffffff` | Page/section background |
| `--default-color` | `#444444` | Body text |
| `--heading-color` | `#012970` | Headings, titles |
| `--accent-color` | `#4154f1` | Links, buttons, highlights, brand |
| `--surface-color` | `#ffffff` | Card/box backgrounds |
| `--contrast-color` | `#ffffff` | Text on accent/heading backgrounds |

**Navigation colors** (`main.css:19-27`):

| Variable | Role |
|----------|------|
| `--nav-color` | `#012970` — nav link default |
| `--nav-hover-color` | `#4154f1` — nav link hover/active |

**Color presets** — apply these classes to `<section>` for alternate backgrounds:

| Class | Effect |
|-------|--------|
| `light-background` | Light gray background, white surface |
| `dark-background` | Dark background, white text |

---

## 2. Typography

Defined in `main.css:3-7`.

| Role | Font Family | CSS Variable |
|------|-------------|--------------|
| Body text / paragraphs | Roboto | `--default-font` |
| All headings (h1–h6) | Nunito | `--heading-font` |
| Navigation links | Poppins | `--nav-font` |

### Font sizes by context

| Element | Size | Weight | Notes |
|---------|------|--------|-------|
| Hero h1 | `48px` | 700 | Desktop; `28px` on mobile |
| Hero p (subtitle) | `20px` | 400 | |
| Section title `<p>` | `32px` | 700 | Large heading under the badge |
| Section title `<h2>` badge | `13px` | 700 | All-caps pill |
| Card h3 | `24px` | 700 | |
| Feature icon-box h4 | `20px` | 700 | |
| Body paragraph | Default (`16px`) | 400 | Inherited from `--default-font` |
| Footer h4 | `16px` | bold | |
| Footer body | `14px` | — | |

---

## 3. Page Shell (Boilerplate)

Every new page follows this structure. Use `_templates/header-inner.html` and `_templates/footer.html`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Meta, fonts, CSS (see header-inner.html) -->
</head>
<body class="[page-name]-page">

  <!-- COPY header-inner.html here -->

  <main class="main">

    <!-- Page Title (with breadcrumbs) -->
    <div class="page-title">
      <div class="heading">
        <div class="container">
          <div class="row d-flex justify-content-center text-center">
            <div class="col-lg-8">
              <h1>Page Title</h1>
              <p class="mb-0">Brief description</p>
            </div>
          </div>
        </div>
      </div>
      <nav class="breadcrumbs">
        <div class="container">
          <ol>
            <li><a href="index.html">Home</a></li>
            <li class="current">Page Title</li>
          </ol>
        </div>
      </nav>
    </div>

    <!-- Page content sections go here -->

  </main>

  <!-- COPY footer.html here -->

</body>
</html>
```

### Body class convention

| Page | Body class |
|------|-----------|
| Homepage | `index-page` |
| Portfolio | `portfolio-page` |
| Contact | `contact-page` |
| Blog | `blog-page` |
| Blog details | `blog-details-page` |

**Important:** The homepage uses `fixed-top` on the header; sub-pages use `sticky-top`. The body class determines transparent header behavior on scroll.

---

## 4. Header

### Homepage Header (`index.html`)

- `class="header d-flex align-items-center fixed-top"`
- Body has `class="index-page"` → transparent header, solid on scroll
- Nav links use hash anchors: `#about`
- Active link: add `class="active"` to whichever is current

### Inner Page Header

- `class="header d-flex align-items-center sticky-top"`
- Always solid background
- Nav links use full paths: `index.html#about`
- No `index-page` body class

### Navigation Links (canonical — 5 links)

```html
<nav id="navmenu" class="navmenu">
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="index.html#about">About</a></li>
    <li><a href="portfolio.html">Portfolio</a></li>
    <li><a href="#">Facilities</a></li>
    <li><a href="contact.html">Contact</a></li>
  </ul>
  <i class="mobile-nav-toggle d-xl-none bi bi-list"></i>
</nav>
```

### Logo Markup

```html
<a href="index.html" class="logo d-flex align-items-center me-auto">
  <img src="assets/img/logo.png" alt="">
  <h1 class="sitename">Tissue Culture</h1>
</a>
```

---

## 5. Footer

Use `_templates/footer.html`. It includes:
- Newsletter subscription
- Footer-about (Tissue Culture branding)
- Useful Links (5 nav links)
- Our Services (Plants Growth Room, Green House, Contract Production)
- Follow Us (social icons)
- Copyright bar

Do **not** add BootstrapMade credit text, template links, or FlexStart branding. The copyright bar uses:
```html
<p>&copy; <span>Copyright</span> <strong class="px-1 sitename">Tissue Culture</strong> <span>All Rights Reserved</span></p>
```

---

## 6. Section Title Pattern

Every section uses this exact structure:

```html
<div class="container section-title" data-aos="fade-up">
  <h2>SECTION_LABEL</h2>
  <p>Large Descriptive Title<br></p>
</div>
```

- `<h2>`: All-caps badge (13px, accent-color background pill)
- `<p>`: Large heading (32px, heading-color, 700 weight, Nunito)
- Always wrapped in `<div class="container section-title">`
- Always has `data-aos="fade-up"`

---

## 7. Card Pattern

Used in Values, Services, and any card-based section.

```html
<div class="col-lg-4" data-aos="fade-up" data-aos-delay="100">
  <div class="card">
    <img src="assets/img/example.jpg" class="img-fluid" alt="">
    <h3>Card Title</h3>
    <p>Card description text here.</p>
  </div>
</div>
```

CSS properties applied to cards (already in `main.css`):
- `background-color: var(--surface-color)`
- `box-shadow: 0px 0 10px rgba(0, 0, 0, 0.1)`
- `padding: 30px`
- `border: 0`
- `transition: 0.3s`
- `height: 100%`
- Hover: larger shadow

---

## 8. Service Item Cards

```html
<div class="col-lg-4 col-md-6" data-aos="fade-up" data-aos-delay="100">
  <div class="service-item item-cyan position-relative">
    <i class="bi bi-brightness-high icon"></i>
    <h3>Service Name</h3>
    <p>Service description.</p>
  </div>
</div>
```

Available color variants: `item-cyan`, `item-orange`, `item-teal`, `item-red`, `item-indigo`, `item-pink`
Colors are: cyan (`#0dcaf0`), orange (`#fd7e14`), teal (`#20c997`), red (`#df1529`), indigo (`#6610f2`), pink (`#f3268c`)

---

## 9. Buttons

### Primary CTA (hero, contact form submit)

```html
<a href="#link" class="btn-get-started">Button Text <i class="bi bi-arrow-right"></i></a>
<button type="submit">Send Message</button>  <!-- inside .php-email-form -->
```

### Read More (blog, services)

```html
<a href="#" class="read-more stretched-link">
  <span>Read More</span> <i class="bi bi-arrow-right"></i>
</a>
```

### Outline Button (pricing)

```html
<a href="#" class="btn-buy">Buy Now</a>
```

---

## 10. Forms

### Contact Form

```html
<form action="forms/contact.php" method="post" class="php-email-form" data-aos="fade-up" data-aos-delay="200">
  <div class="row gy-4">
    <div class="col-md-6">
      <input type="text" name="name" class="form-control" placeholder="Your Name" required="">
    </div>
    <div class="col-md-6">
      <input type="email" class="form-control" name="email" placeholder="Your Email" required="">
    </div>
    <div class="col-12">
      <input type="text" class="form-control" name="subject" placeholder="Subject" required="">
    </div>
    <div class="col-12">
      <textarea class="form-control" name="message" rows="6" placeholder="Message" required=""></textarea>
    </div>
    <div class="col-12 text-center">
      <div class="loading">Loading</div>
      <div class="error-message"></div>
      <div class="sent-message">Your message has been sent. Thank you!</div>
      <button type="submit">Send Message</button>
    </div>
  </div>
</form>
```

### Newsletter Form

```html
<form action="forms/newsletter.php" method="post" class="php-email-form">
  <div class="newsletter-form"><input type="email" name="email"><input type="submit" value="Subscribe"></div>
  <div class="loading">Loading</div>
  <div class="error-message"></div>
  <div class="sent-message">Your subscription request has been sent. Thank you!</div>
</form>
```

### Contact Info Items

```html
<div class="info-item" data-aos="fade" data-aos-delay="200">
  <i class="bi bi-geo-alt"></i>
  <h3>Address</h3>
  <p>Address Line 1</p>
  <p>Address Line 2</p>
</div>
```

Available icons: `bi-geo-alt` (address), `bi-telephone` (phone), `bi-envelope` (email), `bi-clock` (hours)

---

## 11. Stats Counter

```html
<div class="stats-item d-flex align-items-center w-100 h-100">
  <i class="bi bi-emoji-smile color-blue flex-shrink-0"></i>
  <div>
    <span data-purecounter-start="0" data-purecounter-end="58" data-purecounter-duration="1" class="purecounter"></span>
    <p>Label</p>
  </div>
</div>
```

---

## 12. Image Conventions

| Location | Pattern/Format | Notes |
|----------|---------------|-------|
| Hero | `assets/img/heroimage.jpg` | Full-width hero image |
| About / Features | `assets/img/features1.jpeg` | Side image, `.img-fluid` |
| Section cards | `assets/img/values-1.jpeg` | Card image |
| Team | `assets/img/team/team-1.jpg` | 400×400-ish portrait |
| Portfolio | `assets/img/portfolio/app-1.jpg` | Gallery thumbnails |
| Blog | `assets/img/blog/blog-1.jpg` | Post featured images |
| Clients/Logo | `assets/img/clients/client-1.png` | Swiper carousel |
| Logo | `assets/img/logo.png` | 36px max-height in header |

Common classes: `.img-fluid` for responsive images, `.animated` for hero animation.

---

## 13. AOS Animation Conventions

All elements animate on scroll. Standard delays:

| Position in row | `data-aos-delay` |
|----------------|-------------------|
| 1st item | `100` |
| 2nd item | `200` |
| 3rd item | `300` |
| 4th item | `400` |

Animations used: `fade-up`, `zoom-out`, `zoom-in`, `fade`

---

## 14. Required Scripts & CSS (every page)

### CSS (in `<head>`, this order):

```html
<link href="assets/vendor/bootstrap/css/bootstrap.min.css" rel="stylesheet">
<link href="assets/vendor/bootstrap-icons/bootstrap-icons.css" rel="stylesheet">
<link href="assets/vendor/aos/aos.css" rel="stylesheet">
<link href="assets/vendor/glightbox/css/glightbox.min.css" rel="stylesheet">
<link href="assets/vendor/swiper/swiper-bundle.min.css" rel="stylesheet">
<link href="assets/css/main.css" rel="stylesheet">
```

### JS (before `</body>`, this order):

```html
<script src="assets/vendor/bootstrap/js/bootstrap.bundle.min.js"></script>
<script src="assets/vendor/php-email-form/validate.js"></script>
<script src="assets/vendor/aos/aos.js"></script>
<script src="assets/vendor/glightbox/js/glightbox.min.js"></script>
<script src="assets/vendor/purecounter/purecounter_vanilla.js"></script>
<script src="assets/vendor/imagesloaded/imagesloaded.pkgd.min.js"></script>
<script src="assets/vendor/isotope-layout/isotope.pkgd.min.js"></script>
<script src="assets/vendor/swiper/swiper-bundle.min.js"></script>
<script src="assets/js/main.js"></script>
```

### Google Fonts (in `<head>`):

```html
<link href="https://fonts.googleapis.com" rel="preconnect">
<link href="https://fonts.gstatic.com" rel="preconnect" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Nunito:ital,wght@0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap" rel="stylesheet">
```

---

## 15. Quick Reference: Creating a New Page

1. Copy the full content of `_templates/header-inner.html`
2. Replace `[PAGE_CLASS]` with the body class
3. Replace `[TITLE]`, `[DESCRIPTION]`, `[KEYWORDS]`
4. Mark the active nav link with `class="active"`
5. Add your page content inside `<main class="main">` after the comment
6. Copy the full content of `_templates/footer.html` after your content
7. Never add FlexStart/BootstrapMade credits, links, or branding
