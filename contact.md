---
layout: page
title: Contact
permalink: /contact/
---

## Get in Touch

Use the form below to send me a message. I'll reply via email as soon as possible.

<form action="https://formspree.io/f/your-form-id" method="POST" style="max-width: 600px; margin: 2rem auto;">
  <div style="margin-bottom: 1.5rem;">
    <label for="name" style="display: block; margin-bottom: 0.5rem; font-weight: 600;">Your Name</label>
    <input type="text" name="name" id="name" required style="width: 100%; padding: 0.8rem; border: 1px solid var(--border); border-radius: 6px; background: var(--surface); color: var(--text);">
  </div>

  <div style="margin-bottom: 1.5rem;">
    <label for="email" style="display: block; margin-bottom: 0.5rem; font-weight: 600;">Your Email (required for reply)</label>
    <input type="email" name="_replyto" id="email" required style="width: 100%; padding: 0.8rem; border: 1px solid var(--border); border-radius: 6px; background: var(--surface); color: var(--text);">
  </div>

  <div style="margin-bottom: 1.5rem;">
    <label for="message" style="display: block; margin-bottom: 0.5rem; font-weight: 600;">Message</label>
    <textarea name="message" id="message" rows="6" required style="width: 100%; padding: 0.8rem; border: 1px solid var(--border); border-radius: 6px; background: var(--surface); color: var(--text); resize: vertical;"></textarea>
  </div>

  <button type="submit" style="background: var(--accent); color: white; padding: 0.9rem 2rem; border: none; border-radius: 8px; font-weight: 600; cursor: pointer; transition: background 0.3s;">
    Send Message
  </button>
</form>

<p style="text-align: center; margin-top: 2rem; color: var(--text-muted); font-size: 0.95rem;">
  Powered by <a href="https://formspree.io" style="color: var(--accent);">Formspree</a> — your message is sent securely to my inbox.
</p>
