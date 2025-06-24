# Markdoc Configuration Test Document

This document tests all the custom Markdoc nodes and tags defined in the markdoc configuration.

# Columns and Cards
{% column %}

{% card title="this is the left card" description="this is me trying" %}
{% /card %}

{% card title="this is the right card" description="this is me trying" %}
{% /card %}

{% /column %}

--- 
# Callouts
preset definitions for callouts include: info, warning, error, success, tip, AND danger
{% callout title="this is info "%}
info callout
{% /callout %}

{% callout title="this is a warning" type="warning"%}
warning callout
{% /callout %}

{% callout title="this is an error" type="error"%}
error callout
{% /callout %}

{% callout title="the pathway to success" type="success"%}
success callout
{% /callout %}

{% callout title="this is a tip" type="tip"%}
tip callout
{% /callout %}

{% callout title="this is danger" type="danger"%}
danger callout
{% /callout %}