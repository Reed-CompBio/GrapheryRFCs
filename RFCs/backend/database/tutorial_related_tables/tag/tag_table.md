# `Tag` Table

`Tag` is a concrete tag model referenced by both `TutorialAnchor` and `GraphAnchor`.

## Mixins

* [`UUIDMixin`](/RFCs/backend/database/mixins.md#UUIDMixin)
* [`TimeDateMixin`](/RFCs/backend/database/mixins.md#TimeDateMixin)

|     Field     |                   Type                   |                Description                |
| :-----------: | :--------------------------------------: | :---------------------------------------: |
|    `name`     |            `models.CharField`            | The name of the tag, shown to the public. |
| `tag_anchor`  | [`FK(TagAnchor)`](./tag_anchor_table.md) |       The anchor point of the tag.        |
| `description` |            `models.TextField`            |       The description of this tag.        |
