# Markdoc Configuration Test Document

This document tests all the custom Markdoc nodes and tags defined in the markdoc configuration.

# Columns and Cards
{% column %}

{% card title="Left Card with Default Icon" description="Testing default text icon" %}
This card uses the default "text" icon and should display properly.
{% /card %}

{% card title="Right Card Custom" description="Another card for column testing" icon="text" %}
This card explicitly sets the text icon.
{% /card %}

{% /column %}

{% column cols=3 gap="lg" %}

{% card title="Card 1" description="First of three" %}
Content for first card
{% /card %}

{% card title="Card 2" description="Second of three" %}
Content for second card
{% /card %}

{% card title="Card 3" description="Third of three" %}
Content for third card
{% /card %}

{% /column %}

---

# Callouts
Preset definitions for callouts include: info, warning, error, success, tip, AND danger

{% callout title="Information Callout" type="info" %}
This is an info callout with blue styling
{% /callout %}

{% callout title="Warning Callout" type="warning" %}
This is a warning callout with yellow/orange styling
{% /callout %}

{% callout title="Error Callout" type="error" %}
This is an error callout with red styling
{% /callout %}

{% callout title="Success Callout" type="success" %}
This is a success callout with green styling
{% /callout %}

{% callout title="Tip Callout" type="tip" %}
This is a tip callout with helpful information
{% /callout %}

{% callout title="Danger Callout" type="danger" %}
This is a danger callout for critical warnings
{% /callout %}

{% callout title="Default Callout" %}
This callout has no type specified, should use default styling
{% /callout %}

---

# Accordion Components

{% accordion title="Basic Accordion" description="This is a basic accordion" %}
This accordion starts closed by default. It contains paragraph content that should be collapsible.

You can put any content inside accordions including lists:
- Item 1
- Item 2
- Item 3
{% /accordion %}

{% accordion title="Open by Default" description="This accordion starts open" defaultOpen=true %}
This accordion starts in the open state because defaultOpen is set to true.

## Heading inside accordion
Accordions can contain headings and other rich content.

```javascript
// Even code blocks work
const example = "code in accordion";
```
{% /accordion %}

{% accordion title="Accordion with Icon" description="Testing icon attribute" icon="star" %}
This accordion has an icon specified. The icon handling might need to be implemented similar to cards.
{% /accordion %}

{% accordion title="Minimal Accordion" %}
This accordion only has a title, using defaults for other attributes.
{% /accordion %}

---

# Break Components

This is content before a default break.

{% break %}

This content comes after a level 3 break (default).

{% break level=1 %}

This content comes after a level 1 break (should be minimal spacing).

{% break level=5 %}

This content comes after a level 5 break (should be maximum spacing).

---

# Complex Nested Examples

{% column cols=2 gap="md" %}

{% accordion title="Accordion in Column" description="Testing nested components" %}
This accordion is inside a column layout.

{% callout title="Nested Callout" type="success" %}
This callout is nested inside an accordion which is inside a column.
{% /callout %}

More content in the accordion.
{% /accordion %}

{% card title="Card in Same Column" description="Side by side with accordion" %}
This card is in the same column as the accordion above.

## Heading in Card
Cards support rich content too.

{% break level=2 %}

Content after a break inside the card.
{% /card %}

{% /column %}

{% break level=4 %}

## All Callout Types in Columns

{% column cols=2 gap="sm" %}

{% callout title="Info in Column" type="info" %}
Info callout in left column
{% /callout %}

{% callout title="Warning in Column" type="warning" %}
Warning callout in right column
{% /callout %}

{% callout title="Error in Column" type="error" %}
Error callout in left column
{% /callout %}

{% callout title="Success in Column" type="success" %}
Success callout in right column
{% /callout %}

{% callout title="Tip in Column" type="tip" %}
Tip callout in left column
{% /callout %}

{% callout title="Danger in Column" type="danger" %}
Danger callout in right column
{% /callout %}

{% /column %}

---

# Final Comprehensive Test

{% column cols=1 %}

{% card title="Everything Combined" description="Testing all features together" %}

## Card Content with Everything

{% accordion title="Accordion Inside Card" defaultOpen=true %}
This tests accordion inside card functionality.

{% callout title="Triple Nested!" type="tip" %}
Callout inside accordion inside card inside column!
{% /callout %}
{% /accordion %}

{% break level=3 %}

More card content after the accordion and break.

{% /card %}

{% /column %}

## Test Summary

This document tests:
- ✅ **Paragraph nodes** (custom Paragraph component)
- ✅ **Heading nodes** (all levels with Heading component)  
- ✅ **Callout tags** (all 6 types: info, warning, error, success, tip, danger)
- ✅ **Card tags** (with default icon, titles, descriptions)
- ✅ **Break tags** (levels 1, 3, 5)
- ✅ **Column tags** (1, 2, 3 columns with different gaps)
- ✅ **Accordion tags** (default closed, default open, with icons)
- ✅ **Complex nesting** (accordions in cards in columns)
- ✅ **All attribute combinations** (defaults and custom values)