# Implementing domain specific languages in Django Applications

Why would you do that? Aren't they old?

Initial motivation:

- Searching contacts.
- In X and Y but not Z
- Checks evolve over time so we can't hard code them
- Some concepts are very hard do to in GUIs. They can be limited to a linear
  flow of actions.

Really why:

- It's not as hard as you think
- but it is fun! (just don't tell the client)

Might not be for everyone, but you have power users (who can then make
add-ons...?)

### How?

What do we need?

- Lexer
- Parser
- Backend

Lexer and Parser are actually quite generic, so use something which does them.
You can use a code generator. (see below)

Backend is the Django ORM in this example.

### PLY

An implementation of lex and yacc in Python. Naming conventions and code
introspection results in very economic code.

Let's use it to compile expressions like:

    groups__name="XXX" AND NOT groups__name="YYY"
    (modified > 1/4/2011 OR NOT state__name="ok") AND groups__name="XXX"

into `django.models.db.Q` objects.

### Much code...

My interest died right around someone used a docstring for functionality.
That's BAAAD.
