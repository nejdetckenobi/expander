# Expander

Expander is a minimal, selection-based text expansion utility for Linux (X11).

Instead of running as a background daemon or relying on typed triggers, Expander works on **explicit user action**:

- You select a placeholder text
- You press a keyboard shortcut
- The selected text is expanded into a predefined value

The tool is intentionally simple, silent, and predictable.

---

## How It Works

1. You select a piece of text (the *key*) in any editable field
2. Expander looks up this key in a local registry file
3. If a matching value is found:
   - The value is temporarily copied to the clipboard
   - It is pasted at the cursor position
   - Your previous clipboard content is restored

If there is no selection or no matching key, Expander exits without doing anything.

---

## Installation

### Requirements

- Linux (X11 session)
- `bash`
- `xclip`
- `xdotool`
- `jq`

Wayland is **not supported**.

### Install Steps

1. Save the script somewhere in your `$PATH`, for example:
   ```bash
   ~/bin/expander
   ```

2. Make it executable:
   ```bash
   chmod +x ~/bin/expander
   ```

3. Run it once to initialize configuration:
   ```bash
   expander
   ```

This will automatically create the registry file if it does not exist.

---

## Keyboard Shortcut (Recommended)

Expander is designed to be used via a keyboard shortcut.

A good default is:

**`Super + E`**  (E for *Expand*)

Reasons for this choice:
- Easy to remember
- Low risk of accidental triggering
- Fits the explicit “select → expand” workflow

Bind this shortcut using your desktop environment, or a tool like `sxhkd` or `xbindkeys`.

---

## Usage

1. Type a placeholder (for example: `ADDR`, `EMAIL`, `COMPANY_NAME`)
2. Select it (mouse or keyboard)
3. Press **`Super + E`**

If the placeholder exists in the registry, it will be replaced with its expanded value.

You can undo the operation immediately using `Ctrl + Z`.

---

## Registry

The registry is a simple JSON file located at:

```
~/.config/expander/registry.json
```

Example:

```json
{
  "ADDR": "221B Baker Street, London",
  "EMAIL": "user@example.com",
  "COMPANY": "Example Corp"
}
```

- Keys are matched **exactly** against the selected text
- Values can be any string
- The file can be edited with any text editor

The registry file is created automatically with an empty JSON object (`{}`) on first run.

---

## Limitations

- Linux only
- X11 only (Wayland is not supported)
- Does **not** work reliably in terminal emulators
- Depends on PRIMARY selection (explicit selection is required)

This tool does not run in the background and does not monitor keystrokes.

---

## Security Notice

The registry file is **plain text**.

Do **not** store sensitive or secret information such as:
- Real credit card numbers
- Bank account details
- Passwords or tokens
- Personal data you are not comfortable exposing

Expander is **not a password manager** and provides no encryption or access control.

Use it only for data you are comfortable keeping in clear text.

---

## Philosophy

Expander favors:
- Explicit user action over automation
- Simplicity over features
- Predictable behavior over magic

It is meant to stay small, understandable, and easy to remove if you ever stop using it.

