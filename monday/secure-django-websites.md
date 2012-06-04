# Building secure django websites

- integrity - internal consistency or lack or corruption
- confidentiality - keep stuff secret
- available - able to be used or obtained

### How cookies and sessions work

- Set-cookie: name=value. Set that cookie in the browsers cookie jar.
- Sent back if the relevant information is ok. (Domain, Path, Secure)
- This happens always - doesn't matter what it's actually doing.
- They're in the browser, so it's easy to manipulate them.
- So we fix this by setting sessionid as a hash, and storing the information on
  the database. It's **really** important to keep these secret.

### CSRF

- Sends a form from somewhere else to your website. Oops, they posted to the
  bank.
- Django kills this with the CSRF token. **USE POST!!!**

### XSS injection

- Dumping a script tag into the page (or similar). 

### Django

- Django does most of this stuff for us. Hooray!
- But be careful! For example your JS is not auto-escaped. Use |escapejs.
- Cookie Security: HTTPOnly. Disable TRACE on your web server. Be careful about
  the path the cookie is set for.

### Server side injections

- SQL injection
- The ORM solves this. But if you run custom stuff, be CAREFUL. Use prepared
  statements.
- But there's more than just SQL. Equally any other back end system, such as
  other databases, Redis, shell (`rm -rf /`!)

### Trusting the browser

- Browsers are friends! Or are they? Everything can be compromised. Browser
  headers, cookies, user agents, anything else is not to be trusted.

### Other issues

- Be careful with model forms.
- If you're being explicit about which fields to display, be *VERY* careful
  with model forms. Perhaps better *not* to use the exclude tag at all.

- Don't use plaintext passwords!
- Limit the number of attempts (django-axes, django-logout)
- If you use logins, use SSL
- If you use SSL, look at django-secure.

- Clickjacking. It sucks. There's an optional protection in Django 1.4 which
  stops (hopefully) websites being put in frames.

### Backups

- Who runs restores? Need to do that!
- Who keeps their backups elsewhere?
