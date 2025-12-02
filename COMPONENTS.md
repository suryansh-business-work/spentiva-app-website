# Spentiva Component Library - Usage Guide

## Form Components

### Input Component

```astro
import Input from "../components/forms/Input.astro";

<!-- Basic text input -->
<Input
  name="username"
  label="Username"
  placeholder="Enter your username"
  required
/>

<!-- Email with validation -->
<Input
  type="email"
  name="email"
  label="Email Address"
  placeholder="you@example.com"
  required
  error="Please enter a valid email"
/>

<!-- With helper text -->
<Input
  name="phone"
  label="Phone Number"
  helperText="We'll never share your phone number"
  autocomplete="tel"
/>
```

### Button Component

```astro
import Button from "../components/forms/Button.astro";

<!-- Primary button -->
<Button variant="primary" type="submit">
  Submit Form
</Button>

<!-- With icon -->
<Button variant="primary" icon="fas fa-rocket" iconPosition="left">
  Get Started
</Button>

<!-- Loading state -->
<Button variant="primary" loading>
  Processing...
</Button>

<!-- Outline variant -->
<Button variant="outline" size="lg">
  Learn More
</Button>

<!-- Full width -->
<Button variant="secondary" fullWidth>
  Sign Up
</Button>
```

### Textarea Component

```astro
import Textarea from "../components/forms/Textarea.astro";

<!-- Basic textarea -->
<Textarea
  name="message"
  label="Your Message"
  rows={6}
  placeholder="Tell us what you think..."
/>

<!-- With character counter -->
<Textarea
  name="bio"
  label="Bio"
  maxLength={500}
  helperText="Tell us about yourself"
  required
/>
```

---

## UI Components

### Image Component

```astro
import Image from "../components/ui/Image.astro";

<!-- Basic usage -->
<Image
  src="/images/hero.jpg"
  alt="Hero banner"
  width={1200}
  height={600}
/>

<!-- With custom fallback -->
<Image
  src="https://example.com/image.jpg"
  alt="External image"
  fallbackSrc="/images/custom-placeholder.svg"
  loading="eager"
/>

<!-- Lazy loaded with object fit -->
<Image
  src="/images/team-photo.jpg"
  alt="Our team"
  class="rounded-xl"
  objectFit="cover"
  loading="lazy"
/>
```

**Features:**
- Automatic broken image detection
- Falls back to placeholder on error
- Lazy loading by default
- Displays loading placeholder

---

### CookieConsent Component

```astro
import CookieConsent from "../components/ui/CookieConsent.astro";

<!-- Add to BaseLayout (already integrated) -->
<body>
  <slot />
  <CookieConsent />
</body>
```

**Features:**
- Auto-displays on first visit
- Stores preference in localStorage
- 365-day expiry
- Accept/Decline options
- Smooth slide-in animation

**JavaScript API:**
```javascript
// Check if user has accepted cookies
const consent = localStorage.getItem('spentiva_cookie_consent');
if (consent === 'accepted') {
  // Initialize analytics
}
```

---

### Alert Component

```astro
import Alert from "../components/ui/Alert.astro";

<!-- Info alert -->
<Alert variant="info" title="Did you know?">
  You can save up to 20% with our yearly plan!
</Alert>

<!-- Success message -->
<Alert variant="success" dismissible>
  Your message has been sent successfully!
</Alert>

<!-- Warning with custom icon -->
<Alert variant="warning" icon="fas fa-exclamation-circle">
  This action cannot be undone.
</Alert>

<!-- Error alert -->
<Alert variant="error" title="Error">
  Something went wrong. Please try again.
</Alert>
```

---

### Badge Component

```astro
import Badge from "../components/ui/Badge.astro";

<!-- Default badge -->
<Badge>New</Badge>

<!-- Primary badge -->
<Badge variant="primary" size="md">
  Popular
</Badge>

<!-- Success badge -->
<Badge variant="success" rounded={false}>
  Verified
</Badge>

<!-- In context -->
<h2>
  Premium Plan
  <Badge variant="warning">Save 17%</Badge>
</h2>
```

---

### Card Component

```astro
import Card from "../components/ui/Card.astro";

<!-- Elevated card -->
<Card variant="elevated" padding="lg">
  <h3>Card Title</h3>
  <p>Card content goes here...</p>
</Card>

<!-- Outlined card with hover -->
<Card variant="outlined" hoverable>
  <h3>Hover Me</h3>
  <p>I'll lift up on hover!</p>
</Card>

<!-- Clickable card -->
<Card variant="filled" clickable padding="xl">
  <h3>Click This Card</h3>
  <p>Cursor will show pointer on hover</p>
</Card>
```

---

## Complete Form Example

```astro
---
import Input from "../components/forms/Input.astro";
import Textarea from "../components/forms/Textarea.astro";
import Button from "../components/forms/Button.astro";
import Alert from "../components/ui/Alert.astro";
---

<form method="POST" class="space-y-6">
  <Alert variant="info">
    All fields marked with * are required.
  </Alert>

  <Input
    type="text"
    name="name"
    label="Full Name"
    placeholder="John Doe"
    required
  />

  <Input
    type="email"
    name="email"
    label="Email Address"
    placeholder="john@example.com"
    required
  />

  <Input
    type="tel"
    name="phone"
    label="Phone Number"
    placeholder="+1 (555) 123-4567"
    helperText="Include country code"
  />

  <Textarea
    name="message"
    label="Your Message"
    rows={6}
    maxLength={1000}
    placeholder="Tell us how we can help..."
    required
  />

  <div class="flex gap-4">
    <Button variant="primary" type="submit" icon="fas fa-paper-plane">
      Send Message
    </Button>
    <Button variant="outline" type="reset">
      Clear Form
    </Button>
  </div>
</form>
```

---

## Accessibility Features

All components include:

✅ **ARIA Labels**
- `aria-label` for screen readers
- `aria-invalid` for form errors
- `aria-describedby` for help text
- `aria-live` for dynamic updates

✅ **Keyboard Navigation**
- Tab order follows visual order
- Enter/Space activates buttons
- Escape dismisses alerts

✅ **Focus Management**
- Visible focus indicators
- `focus:ring-2` for all interactive elements
- Proper focus trap in modals

✅ **Error States**
- Visual error indicators (red border)
- Error messages with `role="alert"`
- Descriptive error text

---

## Best Practices

1. **Always provide alt text for images**
   ```astro
   <Image src="/hero.jpg" alt="Descriptive alt text" />
   ```

2. **Use semantic button types**
   ```astro
   <Button type="submit">Submit</Button>  ✅
   <Button type="button">Cancel</Button>  ✅
   ```

3. **Label all form inputs**
   ```astro
   <Input name="email" label="Email" />  ✅
   ```

4. **Provide helper text for complex fields**
   ```astro
   <Input
     name="password"
     helperText="Must be at least 8 characters"
   />
   ```

5. **Use appropriate alert variants**
   - `info` - General information
   - `success` - Success messages
   - `warning` - Warnings, cautions
   - `error` - Error messages, failures
