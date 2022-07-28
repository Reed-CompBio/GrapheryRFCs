# `TagAnchor` Table

The tag anchor table stores tags' anchor points. Graph anchors and tutorial anchors share the same anchor table.

## Mixins

* [`UUIDMixin`](/RFCs/backend/database/mixins.md#UUIDMixin)
* [`TimeDateMixin`](/RFCs/backend/database/mixins.md#TimeDateMixin)
* [`StatusMixin`](/RFCs/backend/database/mixins.md#StatusMixin)

|     Field     |        Type        |       Description       |
| :-----------: | :----------------: | :---------------------: |
| `anchor_name` | `models.CharField` | The name of the anchor. |
