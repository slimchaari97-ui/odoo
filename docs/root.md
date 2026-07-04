# Odoo 19 Predefined Community Engine Master Map

> **CRITICAL AI SYSTEM RULE**: The root directory (`/`) of this workspace contains the full, unaltered, native source code of the **Odoo 19 Community Edition**. An AI assistant reading this workspace **cannot inspect individual project files** and **must rely entirely on this documentation matrix** to understand the pre-existing environment. At this moment, **no custom applications or modules have been created yet**. All subsequent feature requests must target new, isolated custom addon paths (e.g., `/custom_addons/`) using safe framework inheritance, leaving the base workspace untouched.

---

## 1. Native Framework & Filesystem Core Layout

Treat the following structure under `/` as the immutable upstream community baseline:

* `/odoo/`: The engine core. Contains the Object-Relational Mapping (ORM) engine, abstract fields definitions (`/odoo/fields.py`), base WSGI/HTTP routing machinery (`/odoo/http.py`), multi-tenancy management, security rule parsing, and QWeb view compilation rules.
* `/addons/`: The predefined native base applications bundled with Odoo 19 Community Edition. This is where standard, out-of-the-box business models are situated.
* `/odoo-bin`: The executable orchestration script used to boot the application server, invoke tests, update components (`-u`), or pass runtime parameters like custom directory paths (`--addons-path`).

---

## 2. Directory Matrix of Predefined Core Community Addons

When future tasks ask you to reference or inherit from out-of-the-box flows, target these native components residing within `/addons/`:

| Core Technical Name | Business & Logic Responsibility | Primary Predefined Models | Essential Context Hooks / Architecture |
| :--- | :--- | :--- | :--- |
| **`base`** | Ultimate core blueprint for the environment. Maps systems, geographical layouts, multi-company trees, currencies, and technical users. | `res.partner`<br>`res.company`<br>`res.users`<br>`res.currency`<br>`ir.ui.view`<br>`ir.model` | Must be declared in the dependency configuration (`'depends': ['base']`) of any custom module created down the line. |
| **`mail`** | Houses the enterprise collaboration chatter, record log trails, activity management sub-systems, and social channels. | `mail.thread`<br>`mail.activity.mixin`<br>`mail.followers`<br>`mail.message` | Designed to be inherited as abstract mixins (`_inherit = ['mail.thread', 'mail.activity.mixin']`) to instantly attach audit tracking into tables. |
| **`product`** | Orchestrates catalog master lists, matrix variations, generic unit configurations, and base pricing structures. | `product.template`<br>`product.product`<br>`product.category`<br>`uom.uom` | Serves as the global standard reference for trading, supply chains, warehouses, and material lists. |
| **`analytic`** | Provides dimension-less accounting distribution vectors, operational cost center mapping, and cross-sectional financial tagging. | `analytic.account`<br>`analytic.plan`<br>`analytic.line` | Used to link real-time logs or structural moves directly to business tracking definitions without mutating general ledger charts. |
| **`web`** | Home of the native front-end UI client architecture, system assets, HTTP controllers, and the core OWL framework engine. | Abstract client layers, system notification APIs, layout view controllers | Custom UI additions or component modifications must reference static asset maps under this dependency. |

---

## 3. Mandatory Blueprints for Future Code Generation

When requested in the next prompts to create a module or extension, follow these structural rules sight-unseen:

### A. Modular Scaffolding Blueprint
All new functional extensions must use isolated folders outside the core paths, structured precisely as follows:
```text
custom_addons/your_module_name/
├── __init__.py
├── __manifest__.py
├── models/
│   ├── __init__.py
│   └── custom_model.py
├── security/
│   ├── ir.model.access.csv
│   └── security_groups.xml
└── views/
    └── custom_model_views.xml
```

### B. Safe Modification Logic (Model Inheritance)
Never write direct database alterations. Use classical inheritance (`_inherit`) to attach records to existing community tools safely:

```python
from odoo import models, fields, api

class ResPartner(models.Model):
    _inherit = 'res.partner'  # Inherits the native res.partner model from the base module

    x_custom_reference = fields.Char(string="Custom System ID")
```

### C. UI Modification Blueprint (XPath Injections)
To place view elements on standard community screens, look up or assume standard semantic layouts and inject elements using strict structural positioning coordinates:

```xml
<record id="view_partner_form_inherit_custom" model="ir.ui.view">
    <name>res.partner.form.inherit.custom</name>
    <model>res.partner</model>
    <inherit_id ref="base.view_partner_form"/> <!-- Target predefined core ID -->
    <arch type="xml">
        <xpath expr="//field[@name='vat']" position="after">
            <field name="x_custom_reference"/>
        </xpath>
    </arch>
</record>
```

### D. Security Access Conversion Formula
Every new data sheet requires an entry in `security/ir.model.access.csv`. Translate dot notation strings by replacing periods with underscores and adding `model_` right at the start:
- *Example*: A model named `custom.document` maps to the row ID target `model_custom_document`.

```csv
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
access_custom_doc,access.custom.doc,model_custom_document,base.group_user,1,1,1,1
