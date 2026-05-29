# Issue: `@app.template_filter` decorator silently fails when called without parentheses

## Observed behaviour

The `@app.template_filter` decorator can be used in two ways:

```python
# Style A — with parentheses (explicit name)
@app.template_filter('my_filter')
def my_filter(value):
    ...

# Style B — without parentheses (uses function name)
@app.template_filter
def my_filter(value):
    ...
```

Style A works correctly. Style B silently fails: no error is raised at decoration time, but the filter is never registered with Jinja2. When a template attempts to use `my_filter`, a `TemplateAssertionError` is raised at render time with a message like `No filter named 'my_filter'`.

The silent failure makes this particularly difficult to debug, because the error appears far from where it was caused.

**Minimal reproduction:**

```python
from flask import Flask, render_template_string

app = Flask(__name__)

@app.template_filter          # no parentheses
def shout(value):
    return value.upper()

with app.app_context():
    # This raises TemplateAssertionError: No filter named 'shout'
    result = render_template_string("{{ 'hello' | shout }}")
```

## Expected behaviour

Both calling styles should register the filter correctly:

```python
@app.template_filter          # should work: registers filter named 'shout'
def shout(value):
    return value.upper()

@app.template_filter()        # should also work: same as above
def shout(value):
    return value.upper()

@app.template_filter('shout') # should also work: explicit name
def shout(value):
    return value.upper()
```

If called without parentheses and without arguments, the decorator should detect that it has received a callable directly and treat the callable itself as the filter function, registering it under its `__name__`.

## Notes

- The same issue likely affects `@blueprint.template_filter` since blueprints share the same decorator implementation.
- The fix should not break the existing `@app.template_filter('name')` calling style.
- Look at how similar decorators in the codebase (e.g., `@app.template_test`, `@app.template_global`) handle the with/without-parentheses ambiguity — they may already have a pattern you can follow or extend.
- Adding tests for all three calling styles is expected as part of this fix.
