# Design Guidelines: tmnjnin1x Gaming Community Website

## Design Approach
**Reference-Based**: Gaming/community platforms (Discord, Twitch, Steam) with cyberpunk/futuristic aesthetic emphasizing immersion and energy.

## Core Design Principles
- **Dark Mode First**: Create an immersive gaming atmosphere with deep blacks and neon accents
- **High Energy**: Dynamic animations and glowing effects that convey activity and excitement
- **Data Visualization**: Prominent display of community stats and engagement metrics
- **Community Focus**: Showcase members, events, and content at the forefront

## Typography
- **Primary Font**: 'Orbitron' (Google Fonts) - for headings, title, and emphasis
- **Secondary Font**: 'Poppins' (Google Fonts) - for body text and UI elements
- **Hierarchy**: 
  - Hero title: Extra large, bold, animated
  - Section headings: Large, uppercase, glowing effect
  - Body: Medium weight, high legibility on dark backgrounds
  - Stats/numbers: Bold, oversized for visual impact

## Color Palette
- **Background**: Deep dark/black (#0f0f12)
- **Primary Accent**: Neon Purple (vibrant, glowing)
- **Secondary Accent**: Electric Blue (bright, energetic)
- **Glass Effects**: Translucent white/light overlays with backdrop blur
- **Text**: White/light gray for high contrast

## Layout System
- **Spacing**: Generous padding for breathing room (Tailwind: p-8, p-12, p-16, p-20)
- **Container**: Max-width constrains for readability, full-bleed backgrounds for impact
- **Grid**: Responsive 3-column layouts for stats/cards, 4-column for gallery items

## Component Library

### Hero Section
- Full viewport height with animated particle background OR gradient mesh
- Center-aligned large animated title "tmnjnin1x" with glitch effect
- Subtitle underneath in lighter weight
- Two CTAs: Primary (glowing, neon purple) + Secondary (outlined, electric blue)
- No hero image required - rely on particles/gradient background

### Live Stats Dashboard
- 3 glassmorphic cards in horizontal grid
- Each card: Icon (top), Large number (bold), Label (subtitle)
- Metrics: Voice Hours, Messages Sent, Active Members
- Leaderboard table below: 5 rows with Rank, Avatar (circular), Name, Role badge, XP
- Table styling: Semi-transparent rows with hover glow

### Events Timeline
- Vertical timeline with connecting line
- Each event: Date badge, Event icon, Title, Time details
- Color-coded by event type (gaming nights, tournaments, casual hangouts)
- Cards on alternating sides of timeline (desktop)

### Best Clips Gallery
- 4-column grid (responsive to 2-col tablet, 1-col mobile)
- Video thumbnail placeholders with aspect ratio 16:9
- Play icon overlay (centered, semi-transparent)
- Hover: Scale up (1.05), glow border effect

### Server Rules Accordion
- List of clickable rule headers with chevron icons
- Expand/collapse animation revealing rule details
- Glassmorphic card backgrounds
- Clear visual separation between rules

### Footer
- Multi-column layout: Logo, social links, copyright
- Animated logo element
- Social icons with hover glow
- Dark background matching hero

## Animations (AOS Library)
- **Scroll Triggers**: Fade-in, slide-up for all major sections
- **Hero**: Glitch effect on title (CSS keyframes)
- **Buttons**: Hover glow/ripple effect
- **Cards**: Scale and glow on hover
- **Particles**: Subtle floating/drifting background animation
- **Timeline**: Items fade in as they enter viewport
- **Gallery**: Smooth scale transform on hover

## Visual Effects
- **Glassmorphism**: Translucent backgrounds with `backdrop-filter: blur()` on cards
- **Neon Glow**: Box-shadow with purple/blue accent colors on interactive elements
- **Gradient Mesh**: Animated gradient background alternative to particles
- **Particle System**: Small floating dots/shapes in background (subtle movement)

## Accessibility
- High contrast white text on dark backgrounds
- Interactive elements have clear hover states
- Accordion controls have proper ARIA labels
- Keyboard navigation supported for all interactive elements

## Images
- No large hero image required - use particle/gradient background
- **Gallery Thumbnails**: 16:9 placeholder boxes for video clips (use gradient or dark gray with play icon)
- **Leaderboard Avatars**: Circular profile images (40x40px)
- **Event Icons**: Small category icons for timeline events
- **Footer Logo**: Animated n1x branding element

This design creates an immersive, high-energy gaming community hub with clear information hierarchy, engaging animations, and modern glassmorphic aesthetics that resonate with the Discord gaming audience.