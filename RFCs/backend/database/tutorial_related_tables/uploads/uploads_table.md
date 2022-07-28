# `Uploads` Table

The `Uploads` table contains all the upload file used in the textual tutorial content.

## Mixins

* [`UUIDMixin`](/RFCs/backend/database/mixins.md#UUIDMixin)
* [`TimeDateMixin`](/RFCs/backend/database/mixins.md#TimeDateMixin)

## Fields

|       Fields       |         Type          |             Description             |
| :----------------: | :-------------------: | :---------------------------------: |
|       `file`       |  `models.FileField`   | The file pointer to the actual file |
|       `name`       |  `models.CharField`   |  The descriptive name of the file.  |
| `tutorial_anchors` | `MTM(TutorialAnchor)` |                                     |
|  `graph_anchors`   |  `MTM(GraphAnchor)`   |                                     |
