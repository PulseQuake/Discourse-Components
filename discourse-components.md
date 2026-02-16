# Discourse Reusable Components Reference

---

> **Attribution & License Notice**
>
> This document catalogs reusable UI components extracted from
> [Discourse](https://github.com/discourse/discourse), an open-source
> discussion platform created by Jeff Atwood, Robin Ward, and Sam Saffron.
>
> Discourse is Copyright (C) 2013-2026 Civilized Discourse Construction Kit, Inc.
>
> Discourse is licensed under the **GNU General Public License v2.0 (GPL-2.0)**.
> Any use, modification, or redistribution of the code referenced herein must
> comply with the terms of the GPL-2.0 license. A copy of the license is
> available at: https://www.gnu.org/licenses/old-licenses/gpl-2.0.html
>
> Source Repository: https://github.com/discourse/discourse
>
> All component descriptions, file paths, and architectural details below are
> derived from the Discourse source code. This document is provided for
> educational and reference purposes.

---

## Table of Contents

1. [Rich Text Editor (Composer + ProseMirror)](#1-rich-text-editor-composer--prosemirror)
2. [D-Editor (Markdown Editor)](#2-d-editor-markdown-editor)
3. [Emoji Picker](#3-emoji-picker)
4. [Modal System (DModal)](#4-modal-system-dmodal)
5. [Float Kit (Tooltips, Menus, Toasts)](#5-float-kit-tooltips-menus-toasts)
6. [Select Kit (Dropdowns & Choosers)](#6-select-kit-dropdowns--choosers)
7. [Date & Time Pickers](#7-date--time-pickers)
8. [Upload System (Uppy-Based)](#8-upload-system-uppy-based)
9. [Ace Code Editor](#9-ace-code-editor)
10. [Color Picker](#10-color-picker)
11. [Spreadsheet Editor](#11-spreadsheet-editor)
12. [Form Kit](#12-form-kit)
13. [Avatar System](#13-avatar-system)
14. [Character Counter](#14-character-counter)
15. [SVG Sprite / Icon System](#15-svg-sprite--icon-system)
16. [Lightbox](#16-lightbox)
17. [Bookmark System](#17-bookmark-system)
18. [Component Running Log](#component-running-log)

---

## 1. Rich Text Editor (Composer + ProseMirror)

### Overview
Discourse's rich text editor is a full-featured WYSIWYG writing environment built on top of **ProseMirror**. It powers the forum's post composer with real-time Markdown-to-rich-text conversion, a pluggable extension system, and a configurable toolbar.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/services/composer.js` | Composer service — orchestrates lifecycle (open, close, save drafts) |
| `frontend/discourse/app/components/composer/` | Composer UI components directory |
| `frontend/discourse/app/components/composer/textarea-editor.gjs` | Textarea-based fallback editor |
| `frontend/discourse/app/components/composer/toggle-switch.gjs` | Rich/markdown editor toggle |
| `frontend/discourse/app/components/composer/toolbar-buttons.gjs` | Toolbar button rendering |
| `frontend/discourse/app/lib/composer/toolbar.js` | Toolbar button definitions and registration API |
| `frontend/discourse/app/lib/composer/text-manipulation.js` | ProseMirror text manipulation class (formatting, insertion, selection) |
| `frontend/discourse/app/lib/composer/rich-editor-extensions.js` | Extension registration API for rich editor |
| `frontend/discourse/app/lib/composer/composer-position.js` | Composer positioning logic |
| `frontend/discourse/app/lib/composer/custom-popup-menu-options.js` | Custom popup menu for toolbar |

### ProseMirror Extensions (26 Default)

Located in `frontend/discourse/app/static/prosemirror/extensions/`:

These 26 extensions are auto-registered in `register-default.js`:

| Extension | File | Functionality |
|-----------|------|---------------|
| Emoji | `emoji.js` | Inline emoji rendering and input rules |
| Image | `image.js` | Image embedding, drag-and-drop, resize |
| Onebox | `onebox.js` | URL preview cards (link unfurling) |
| Code (inline) | `code.js` | Inline code formatting with backticks |
| Code Block | `code-block.js` | Fenced code blocks with language selector |
| Link | `link.js` | Hyperlink creation and editing |
| Link Toolbar | `link-toolbar.js` | Floating toolbar for link editing |
| Heading | `heading.js` | H1-H6 heading levels |
| Quote | `quote.js` | Block quotations |
| Hashtag | `hashtag.js` | Category/tag hashtag autocomplete |
| Mention | `mention.js` | @username mention autocomplete |
| Strikethrough | `strikethrough.js` | ~~strikethrough~~ text formatting |
| Underline | `underline.js` | Underline text formatting |
| HTML Inline | `html-inline.js` | Inline HTML passthrough |
| HTML Block | `html-block.js` | Block-level HTML passthrough |
| Trailing Paragraph | `trailing-paragraph.js` | Ensures doc ends with paragraph |
| Typographer Replacements | `typographer-replacements.js` | Smart quotes, dashes, ellipsis |
| Table | `table.js` | Table creation and editing |
| Markdown Paste | `markdown-paste.js` | Paste-as-markdown handler |
| Ordered List | `ordered-list.js` | Numbered lists |
| Bullet List | `bullet-list.js` | Unordered lists |
| Wrap | `wrap.js` | BBCode-style [wrap] blocks |
| Trailing Inline Space | `trailing-inline-space.js` | Whitespace handling |
| Override Drag Ghost | `override-drag-ghost.js` | Custom drag preview |
| Hard Break | `hard-break.js` | Shift+Enter line breaks |
| Grid | `grid.js` | Grid/column layout |

Additional non-default extensions available in the same directory:

| Extension | File | Functionality |
|-----------|------|---------------|
| Placeholder | `placeholder.js` | Editor placeholder text (opt-in) |

### Toolbar Buttons (Default)

| Button | Group | Shortcut | Function |
|--------|-------|----------|----------|
| Bold | fontStyles | Ctrl+B | Wraps selection in `**` |
| Italic | fontStyles | Ctrl+I | Wraps selection in `*` |
| Heading (H1-H4) | fontStyles | Alt+1-4 | Applies heading level with popup submenu |
| Link | insertions | Ctrl+K | Opens link insertion modal |
| Blockquote | insertions | Ctrl+Shift+9 | Applies `> ` prefix |
| Code | insertions | Ctrl+E | Applies inline/block code formatting |
| Bullet List | extras | Ctrl+Shift+8 | Applies `* ` prefix |
| Ordered List | extras | Ctrl+Shift+7 | Applies numbered prefix |

### Recreation Prompt
> Build a rich text editor component using ProseMirror as the editing engine.
> The editor should support a pluggable extension system where each extension
> can define: node specs, mark specs, input rules, keymaps, plugins,
> serializers (to Markdown), and parsers (from Markdown-it tokens). Include a
> configurable toolbar with button groups (fontStyles, insertions, extras),
> keyboard shortcuts, and active state indicators. Support toggling between
> rich text and raw Markdown editing modes. Default extensions should cover:
> bold, italic, headings (H1-H4), links, blockquotes, code/code blocks,
> ordered and unordered lists, images, tables, emoji, @mentions, #hashtags,
> strikethrough, underline, and markdown paste handling.

---

## 2. D-Editor (Markdown Editor)

### Overview
The `d-editor` is Discourse's lower-level editor component that wraps either a plain textarea or the ProseMirror rich editor. It provides the toolbar UI, keyboard shortcut handling, preview rendering, and the text manipulation API that toolbar buttons interact with.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/d-editor.gjs` | Main editor component (862 lines) |
| `frontend/discourse/app/components/d-editor-preview.gjs` | Live HTML preview panel |

### Key Features
- Dual-mode editing (rich text / markdown textarea)
- Live side-by-side preview
- Toolbar with extensible button API
- Keyboard shortcut system with platform-aware modifier keys
- Text manipulation API (applySurround, applyList, formatCode, etc.)
- Plugin event system (`d-editor:toolbar-button-clicked`)

### Recreation Prompt
> Build a dual-mode text editor component that can switch between a ProseMirror
> rich text view and a plain textarea Markdown view. Include a toolbar component
> that renders grouped buttons with icons, labels, keyboard shortcuts, active
> states, and popup submenus. Provide a text manipulation API with methods like
> applySurround(before, after), applyList(prefix), formatCode(), applyHeading(level),
> and toggleDirection(). Add a live preview panel that renders Markdown to HTML.

---

## 3. Emoji Picker

### Overview
A full-featured emoji selection component with search, category tabs, skin tone diversity support, and custom emoji. Renders as a floating menu on desktop and a modal on mobile.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/emoji-picker/index.gjs` | Main picker component (wraps DMenu) |
| `frontend/discourse/app/components/emoji-picker/content.gjs` | Picker content with search, grid, categories (661 lines) |
| `frontend/discourse/app/components/emoji-picker/detached.gjs` | Standalone detached picker |
| `frontend/discourse/app/components/emoji-picker/diversity-menu.gjs` | Skin tone selector |

### Key Features
- Categorized emoji grid (People, Nature, Food, Activities, Travel, Objects, Symbols, Flags)
- Real-time fuzzy search
- Skin tone diversity selector (6 tones)
- Custom emoji support
- Recent/frequently used section
- Mobile-responsive (modal on mobile, popover on desktop)
- Keyboard navigation

### Recreation Prompt
> Build an emoji picker component that displays emoji organized by category in a
> scrollable grid. Include a search bar with fuzzy matching, a skin tone
> diversity menu with 6 tone options, a frequently-used section, and custom emoji
> support. On mobile, render as a full-screen modal; on desktop, render as a
> floating popover anchored to a trigger button. Support keyboard navigation and
> emit a selection callback with the chosen emoji code.

---

## 4. Modal System (DModal)

### Overview
A flexible, accessible modal dialog system with animation, swipe-to-dismiss on mobile, keyboard handling (Escape to close, Enter to confirm), and a slot-based content API.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/d-modal.gjs` | Core modal component (431 lines) |
| `frontend/discourse/app/components/d-modal-cancel.gjs` | Cancel button helper |
| `frontend/discourse/app/components/modal-container.gjs` | Portal container for modals |
| `frontend/discourse/app/components/modal/` | 60+ pre-built modal dialogs |

### Key Features
- Animated entrance/exit (CSS transitions)
- Swipe-to-dismiss on mobile (velocity threshold detection)
- Backdrop click-to-close
- Escape key dismissal
- Enter key triggers primary action
- Focus trapping (tab key cycling within modal)
- Body scroll locking on mobile
- Named content slots: `aboveHeader`, `headerAboveTitle`, `headerBelowTitle`, `belowHeader`, `body`, `footer`, `belowFooter`, `headerPrimaryAction`
- Close initiated tracking (button, ESC, click outside, swipe, programmatic)
- Supports `<div>` or `<form>` as root element
- Flash message integration

### Pre-Built Modals (60+)
Includes: bookmark, flag, share-topic, history, avatar-selector, fast-edit, jump-to-post, keyboard-shortcuts-help, create-invite, spreadsheet-editor, publish-page, edit-topic-timer, and many more.

### Recreation Prompt
> Build a modal dialog system with: animated entrance/exit transitions,
> backdrop overlay with click-to-dismiss, Escape key handling, Enter key
> triggering the primary footer button, focus trapping within the modal,
> swipe-to-dismiss on mobile with velocity threshold, body scroll locking
> on mobile, and a slot-based API for header, body, footer, and surrounding
> content areas. Track how the modal was closed (button, ESC, backdrop,
> swipe). Support both div and form as the modal's root element.

---

## 5. Float Kit (Tooltips, Menus, Toasts)

### Overview
A unified floating UI system providing tooltips, dropdown menus, and toast notifications. Built with Floating UI for positioning.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/float-kit/components/d-tooltip.gjs` | Tooltip component (106 lines) |
| `frontend/discourse/float-kit/components/d-tooltips.gjs` | Tooltip container |
| `frontend/discourse/float-kit/components/d-menu.gjs` | Dropdown menu component (206 lines) |
| `frontend/discourse/float-kit/components/d-menus.gjs` | Menu container |
| `frontend/discourse/float-kit/components/d-toasts.gjs` | Toast notification container |
| `frontend/discourse/float-kit/lib/d-tooltip-instance.js` | Tooltip instance logic |
| `frontend/discourse/float-kit/lib/d-menu-instance.js` | Menu instance logic |
| `frontend/discourse/float-kit/services/tooltip.js` | Tooltip service |
| `frontend/discourse/float-kit/services/menu.js` | Menu service |
| `frontend/discourse/float-kit/services/toasts.js` | Toasts service |

### Key Features

**Tooltips:**
- Hover/focus triggered
- Auto-positioning with Floating UI
- Custom content via slots
- Configurable delay and placement

**Menus:**
- Click-triggered floating panels
- Auto-positioning with collision detection
- Modal fallback on mobile
- Programmatic open/close API
- Custom trigger and content slots

**Toasts:**
- Non-blocking notification system
- Auto-dismiss with configurable duration
- Stacking support for multiple toasts
- Action buttons within toasts

### Recreation Prompt
> Build a floating UI kit with three components: (1) Tooltips that appear on
> hover/focus with auto-positioning and custom content slots; (2) Dropdown
> Menus that open on click with auto-positioning, collision detection, and
> modal fallback on mobile; (3) Toast Notifications that stack vertically,
> auto-dismiss after a timeout, and support action buttons. Use a positioning
> library (e.g., Floating UI) for placement. Expose each as both a component
> and an imperative service API.

---

## 6. Select Kit (Dropdowns & Choosers)

### Overview
A comprehensive dropdown and selection component system with 76 specialized variants. Provides single-select, multi-select, combo boxes, tag choosers, category choosers, and more.

### Source Files

Base components in `frontend/discourse/select-kit/components/`:

| Component | File | Purpose |
|-----------|------|---------|
| Select Kit (base) | `select-kit/select-kit.js` | Core select component |
| Single Select | `single-select.gjs` | Single value selection |
| Multi Select | `multi-select.gjs` | Multiple value selection |
| Combo Box | `combo-box/combo-box.js` | Searchable single select |
| Dropdown Select Box | `dropdown-select-box/dropdown-select-box.js` | Action dropdown |
| Category Chooser | `category-chooser.js` | Forum category selector |
| Category Selector | `category-selector.js` | Multi-category selector |
| Tag Chooser | `tag-chooser.js` | Tag selection with autocomplete |
| User Chooser | `user-chooser/user-chooser.js` | User selection with search |
| Icon Picker | `icon-picker.js` | Icon selection from library |
| Color Palette Picker | `color-palette-picker/color-palette-picker.js` | Color palette selection |
| Font Selector | `font-selector/font-selector.js` | Font family chooser |
| Timezone Input | `timezone-input.js` | Timezone selection |
| Future Date Input | `future-date-input-selector/future-date-input-selector.js` | Future date presets |
| Period Chooser | `period-chooser/period-chooser.js` | Time period selection |
| Notifications Button | `notifications-button/notifications-button.js` | Notification level picker |
| Composer Actions | `composer-actions.js` | Composer action dropdown |

### Key Features
- Filtered/searchable dropdown lists
- Keyboard navigation (arrow keys, Enter, Escape)
- Custom row rendering
- Lazy loading for large datasets
- Selected value display with custom formatters
- Mobile-optimized rendering
- Plugin API for adding custom select kit components

### Recreation Prompt
> Build a modular dropdown selection system with a base SelectKit component
> that supports: single and multi-select modes, searchable/filterable lists,
> keyboard navigation, custom row rendering, lazy loading, and mobile
> optimization. Create specialized variants including: CategoryChooser (with
> color badges and hierarchy), TagChooser (with autocomplete), UserChooser
> (with avatar display), IconPicker (with icon grid), and ComboBox (searchable
> single-select). Support a plugin API for registering new select kit variants.

---

## 7. Date & Time Pickers

### Overview
Date and time selection components with mobile-native fallback. Uses Pikaday on desktop and native HTML date inputs on mobile.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/date-picker.gjs` | Base date picker (122 lines) |
| `frontend/discourse/app/components/date-picker-future.js` | Future dates only (min: tomorrow) |
| `frontend/discourse/app/components/date-picker-past.js` | Past dates only (max: today) |
| `frontend/discourse/app/components/time-input.gjs` | Time selection input |
| `frontend/discourse/app/components/date-time-input.gjs` | Combined date + time picker |
| `frontend/discourse/app/components/date-time-input-range.gjs` | Start/end date-time range |
| `frontend/discourse/app/components/calendar-date-time-input.gjs` | Calendar-style date-time input |

### Key Features
- Pikaday integration for desktop calendar widget
- Native `<input type="date">` on mobile
- i18n for month/day names
- Min/max date constraints
- Future-only and past-only variants
- Combined date-time picker
- Date range selection (start + end)
- YYYY-MM-DD format output

### Recreation Prompt
> Build a date picker component that uses a calendar widget (Pikaday) on
> desktop and falls back to the native HTML date input on mobile. Support
> min/max date constraints, i18n for month/weekday names, and YYYY-MM-DD
> output format. Create variants for future-only dates (min: tomorrow) and
> past-only dates (max: today). Add a time input component and a combined
> date-time picker. Include a date-time range component for selecting
> start and end date-times.

---

## 8. Upload System (Uppy-Based)

### Overview
A file upload system built on Uppy with support for image uploads, drag-and-drop, S3 multipart uploads, chunked uploads, and file validation.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/uppy-image-uploader.gjs` | Image upload component (305 lines) |
| `frontend/discourse/app/components/avatar-uploader.gjs` | Avatar-specific uploader |
| `frontend/discourse/app/components/create-invite-uploader.gjs` | Bulk invite CSV uploader |
| `frontend/discourse/app/components/pick-files-button.gjs` | File picker button |
| `frontend/discourse/app/components/form-template-field/upload.gjs` | Form field upload |
| `frontend/discourse/app/lib/uppy/uppy-upload.js` | Core Uppy upload utility class |
| `frontend/discourse/app/lib/uppy-checksum-plugin.js` | File integrity checksum plugin |
| `frontend/discourse/app/lib/uppy/s3-multipart.js` | S3 multipart upload plugin |
| `frontend/discourse/app/lib/uploads.js` | Upload validation utilities |

### Key Features
- Drag-and-drop upload zones
- Image preview with lightbox
- File type and size validation
- Upload progress indicators
- S3 multipart upload for large files
- SHA-1 checksum verification
- Image dimension tracking (width/height)
- Video upload support (optional)
- CDN URL generation

### Recreation Prompt
> Build a file upload component using the Uppy library. Support drag-and-drop
> upload zones, image preview with dimensions, file type validation (images-only
> mode and general mode), size limits, upload progress indicators, and a delete
> action. Add plugins for SHA-1 checksum verification and S3 multipart uploads
> for large files. Include specialized variants for avatar uploads and bulk
> CSV imports. Generate CDN URLs for uploaded files.

---

## 9. Ace Code Editor

### Overview
An embedded code editor powered by Ace Editor with syntax highlighting, custom theming, CSS color variable detection, and resizable editing area.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/ace-editor.gjs` | Ace editor wrapper (302 lines) |
| `frontend/discourse/app/lib/load-ace-editor.js` | Lazy-loading utility |

### Key Features
- Syntax highlighting for multiple languages (HTML, CSS, JavaScript, SQL, YAML)
- Lazy-loaded (Ace loaded on demand)
- Custom placeholder support with HTML rendering
- CSS color variable detection (highlights Discourse theme variables)
- Resizable via drag handle (grippie)
- Read-only mode
- Auto-save integration
- Custom keyboard shortcut support
- Dark/light theme support

### Recreation Prompt
> Build a code editor component that lazy-loads the Ace Editor library. Support
> syntax highlighting for HTML, CSS, JavaScript, SQL, and YAML. Include a
> draggable resize handle, custom placeholder text, read-only mode, and
> auto-save callbacks. Add CSS color variable detection that highlights theme
> variable references. Support both dark and light editor themes.

---

## 10. Color Picker

### Overview
A color palette selection component that renders a grid of color swatches with selection state and "already used" indicators.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/color-picker.gjs` | Color picker grid (46 lines) |
| `frontend/discourse/app/components/color-picker-choice.js` | Individual color swatch |

### Key Features
- Grid of color swatches
- Check mark on selected color
- "Color used" indicator for already-assigned colors
- Accessible with ARIA group role and labels
- Hex color value output
- Configurable color palette

### Recreation Prompt
> Build a color picker component that displays a grid of color swatches.
> Show a checkmark on the selected color and indicate which colors are
> already in use. Use ARIA group roles for accessibility. Accept a
> configurable array of hex colors and emit the selected color value.

---

## 11. Spreadsheet Editor

### Overview
An in-browser spreadsheet/table editor modal for creating and editing Markdown tables with a spreadsheet-like interface.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/modal/spreadsheet-editor.gjs` | Spreadsheet editor modal (429 lines) |

### Key Features
- Spreadsheet-like cell grid for table editing
- Add/remove rows and columns
- Cell selection and navigation
- Copy/paste support
- Markdown table output generation
- Header row management
- Column alignment controls
- Import data from existing Markdown tables

### Recreation Prompt
> Build a spreadsheet editor component rendered inside a modal dialog.
> Support a cell-based grid with add/remove rows and columns, cell
> selection, copy/paste, header row management, and column alignment.
> Parse existing Markdown tables for editing and serialize back to
> Markdown table format on save.

---

## 12. Form Kit

### Overview
A declarative form-building system with field validation, error display, and consistent layout primitives.

### Source Files

Located in `frontend/discourse/app/form-kit/components/fk/`:

| Component | File | Purpose |
|-----------|------|---------|
| Form | `form.gjs` | Root form component |
| Field | `field.gjs` | Individual form field wrapper |
| Field Data | `field-data.gjs` | Field data binding |
| Control Wrapper | `control-wrapper.gjs` | Input control container |
| Control | `control/` | Input controls directory |
| Label | `label.gjs` | Field label |
| Errors | `errors.gjs` | Field-level error display |
| Errors Summary | `errors-summary.gjs` | Form-level error summary |
| Alert | `alert.gjs` | Form alert messages |
| Char Counter | `char-counter.gjs` | Character count indicator |
| Checkbox Group | `checkbox-group.gjs` | Grouped checkboxes |
| Container | `container.gjs` | Layout container |
| Collection | `collection.gjs` | Repeatable field groups |
| Row | `row.gjs` | Layout row |
| Col | `col.gjs` | Layout column |
| Fieldset | `fieldset.gjs` | Fieldset grouping |
| Input Group | `input-group.gjs` | Grouped inputs |
| Object | `object.gjs` | Nested object fields |
| Meta | `meta.gjs` | Field metadata |
| Optional | `optional.gjs` | Conditional field rendering |

### Recreation Prompt
> Build a declarative form kit with components for: Form (root with validation),
> Field (label + input + errors wrapper), various input Controls, Checkbox
> Groups, Character Counters, Error displays (field-level and summary),
> and layout primitives (Row, Col, Container, Fieldset). Support nested
> object fields, repeatable collections, conditional rendering, and
> form-level alert messages.

---

## 13. Avatar System

### Overview
A comprehensive user avatar display system with upload, flair badges, and multiple size variants.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/user-avatar.gjs` | User avatar display |
| `frontend/discourse/app/components/avatar-flair.gjs` | Group flair badge overlay |
| `frontend/discourse/app/components/user-avatar-flair.gjs` | Combined avatar + flair |
| `frontend/discourse/app/components/avatar-uploader.gjs` | Avatar upload component |
| `frontend/discourse/app/components/user-profile-avatar.gjs` | Profile page avatar |
| `frontend/discourse/app/components/post/avatar.gjs` | Post avatar display |
| `frontend/discourse/app/components/modal/avatar-selector.gjs` | Avatar selection modal |

### Recreation Prompt
> Build an avatar system with components for: displaying user avatars at
> multiple sizes, overlaying group flair badges, uploading new avatars
> with preview, and an avatar selector modal that lets users choose
> between uploaded, generated (letter), and Gravatar avatars.

---

## 14. Character Counter

### Overview
A character count indicator that shows remaining/used characters with visual warning states.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/char-counter.gjs` | Standalone character counter |
| `frontend/discourse/app/form-kit/components/fk/char-counter.gjs` | Form kit integrated counter |

### Recreation Prompt
> Build a character counter component that displays the current count vs.
> maximum allowed characters. Show warning/danger visual states as the
> limit is approached. Support both standalone use and integration
> within a form field wrapper.

---

## 15. SVG Sprite / Icon System

### Overview
A centralized SVG icon system that bundles icons into a single sprite sheet, served with content-based cache keys.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/svg/` | SVG component directory |
| `app/controllers/svg_sprite_controller.rb` | Server-side sprite generation |

### Key Features
- Single SVG sprite sheet with all icons
- Content-hash based cache busting
- Icon helper for template usage
- Theme-aware icon overrides
- Font Awesome icon library integration

### Recreation Prompt
> Build an SVG icon system that bundles individual SVG icons into a single
> sprite sheet. Serve the sprite with content-based cache keys. Provide a
> template helper function that renders icons by name using `<use>` references
> to the sprite. Support icon overrides via theming.

---

## 16. Lightbox

### Overview
An image lightbox/gallery viewer for viewing full-size images from thumbnails.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/lib/lightbox.js` | Lightbox initialization utility |
| `frontend/discourse/app/lib/lightbox/constants.js` | Lightbox configuration constants |
| `frontend/discourse/app/lib/lightbox/quote-image.js` | Quote-embedded image handling |

### Key Features
- Click-to-expand image viewing
- Full-screen overlay
- Image zoom
- Navigation between multiple images
- Keyboard controls (arrow keys, Escape)
- Quote image support

### Recreation Prompt
> Build a lightbox component that expands thumbnail images into a
> full-screen overlay viewer. Support zooming, navigation between
> multiple images with arrow keys, Escape to close, and swipe
> gestures on mobile.

---

## 17. Bookmark System

### Overview
A bookmark/save system with reminder scheduling, quick actions, and custom naming.

### Source Files

| File | Purpose |
|------|---------|
| `frontend/discourse/app/components/bookmark-menu.gjs` | Bookmark quick-action menu |
| `frontend/discourse/app/components/bookmark-icon.gjs` | Bookmark status icon |
| `frontend/discourse/app/components/bookmark-list.gjs` | List of saved bookmarks |
| `frontend/discourse/app/components/bookmark-actions-dropdown.js` | Bookmark action dropdown |
| `frontend/discourse/app/components/modal/bookmark.gjs` | Bookmark creation/edit modal |

### Key Features
- Quick bookmark toggle
- Reminder scheduling (later today, tomorrow, next week, custom)
- Custom bookmark names
- Bookmark list with filtering
- Action dropdown (edit, delete)

### Recreation Prompt
> Build a bookmark system with a quick-toggle button, a creation modal
> with custom naming and reminder scheduling (presets: later today,
> tomorrow, next week, next month, custom date-time), a bookmark list
> view with filtering, and action dropdowns for editing/deleting bookmarks.

---

## Component Running Log

This section tracks all identified extractable components. Components marked with a checkmark have been documented above. Others are candidates for future extraction.

### Documented Components

- [x] Rich Text Editor (ProseMirror Composer)
- [x] D-Editor (Markdown Editor)
- [x] Emoji Picker
- [x] Modal System (DModal)
- [x] Float Kit (Tooltips, Menus, Toasts)
- [x] Select Kit (Dropdowns & Choosers)
- [x] Date & Time Pickers
- [x] Upload System (Uppy)
- [x] Ace Code Editor
- [x] Color Picker
- [x] Spreadsheet Editor
- [x] Form Kit
- [x] Avatar System
- [x] Character Counter
- [x] SVG Sprite / Icon System
- [x] Lightbox
- [x] Bookmark System

### Additional Candidates for Extraction

- [ ] **Topic List** — Forum thread listing with sorting, filtering, pinning (`app/components/topic-list/`)
- [ ] **Topic Timeline** — Scrollable timeline sidebar for navigating long threads (`app/components/topic-timeline/`)
- [ ] **Topic Map** — Summary panel showing participants, links, views (`app/components/topic-map/`)
- [ ] **User Card** — Popup profile card with avatar, bio, stats (`app/components/user-card-contents.gjs`)
- [ ] **Badge System** — Badge display, badge cards, badge titles (`app/components/badge-card.gjs`, `badge-button.gjs`)
- [ ] **Tag List** — Tag display and management (`app/components/tag-list.gjs`)
- [ ] **Breadcrumbs** — Navigation breadcrumb trail (`app/components/bread-crumbs.gjs`)
- [ ] **Flash Messages** — Inline alert/notification messages (`app/components/flash-message.gjs`)
- [ ] **Welcome Banner** — First-visit welcome messaging (`app/components/welcome-banner.gjs`)
- [ ] **User Status** — Online/away/DND status indicator (`app/components/user-status-message.gjs`, `user-status-picker.gjs`)
- [ ] **User Tips** — Onboarding tooltip system (`app/components/user-tip.gjs`, `user-tip-container.gjs`)
- [ ] **Post Text Selection Toolbar** — Floating toolbar on text select (`app/components/post-text-selection-toolbar.gjs`)
- [ ] **Topic Progress** — Reading progress indicator (`app/components/topic-progress.gjs`)
- [ ] **Software Update Prompt** — Version update notification (`app/components/software-update-prompt.gjs`)
- [ ] **Do Not Disturb** — DND scheduling modal (`app/components/modal/do-not-disturb.gjs`)
- [ ] **Time Shortcut Picker** — Quick time selection (later today, tomorrow, etc.) (`app/components/time-shortcut-picker.gjs`)
- [ ] **Password Toggle** — Show/hide password input (`app/components/toggle-password-mask.gjs`)
- [ ] **Category Notification Tracking** — Notification level per category (`app/components/category-notifications-tracking.gjs`)
- [ ] **Async Content** — Loading state wrapper (`app/components/async-content.gjs`)
- [ ] **Conditional Loading Spinner** — Loading indicator (`app/components/conditional-loading-spinner`)
- [ ] **Bulk Actions** — Bulk selection and batch operations (`app/components/bulk-actions/`, `bulk-select-toggle.gjs`)
- [ ] **Sidebar Navigation** — Collapsible sidebar with editable sections (`app/components/sidebar/`)
- [ ] **User Menu** — Notification/profile dropdown menu (`app/components/user-menu/`)
- [ ] **Search** — Full-text search with filters and previews
- [ ] **Poll** — Interactive poll creation and voting (plugin: `plugins/poll/`)
- [ ] **Chat** — Real-time messaging (plugin: `plugins/chat/`)
- [ ] **Discourse Presence** — Typing/composing indicators (plugin: `plugins/discourse-presence/`)

---

> **License & Attribution Footer**
>
> All code referenced in this document is part of the
> [Discourse](https://github.com/discourse/discourse) project.
>
> Copyright (C) 2013-2026 Civilized Discourse Construction Kit, Inc.
>
> This program is free software; you can redistribute it and/or modify it
> under the terms of the GNU General Public License as published by the
> Free Software Foundation; either version 2 of the License, or (at your
> option) any later version.
>
> This program is distributed in the hope that it will be useful, but
> WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
> or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License
> for more details.
>
> You should have received a copy of the GNU General Public License along
> with this program; if not, write to the Free Software Foundation, Inc.,
> 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
>
> Full license text: https://www.gnu.org/licenses/old-licenses/gpl-2.0.html
>
> Discourse is created by Jeff Atwood, Robin Ward, Sam Saffron, and the
> Discourse community. Learn more at https://www.discourse.org/
