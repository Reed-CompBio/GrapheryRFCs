# `TagBase` Table

`TagBase` is an _abstract_ model where all sets of tags must inherit.

## Mixins

*   [`UUIDMixin`](/RFCs/backend/database/mixins.md#UUIDMixin)
*   [`TimeDateMixin`](/RFCs/backend/database/mixins.md#TimeDateMixin)
*   [`StatusMixin`](/RFCs/backend/database/mixins.md#StatusMixin)

|     Field     |                   Type                    |                Description                |
| :-----------: | :---------------------------------------: | :---------------------------------------: |
|    `name`     |            `models.CharField`             | The name of the tag, shown to the public. |
| `tag_anchor`  | [`OTO(TagAnchor)`](./tag_anchor_table.md) |       The anchor point of the tag.        |
| `description` |            `models.TextField`             |       The description of this tag.        |

