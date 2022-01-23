# `TutorialTranslation` Table

Every entry in `TutorialTranslationBase` is linked to one anchor and is the one that's actually holding the textual tutorial . The basic structure of the text content contains a title, paragraphs of actual text in markdown version and html version, an abstract of the main text. It also contains metadata like the authors of the text. 

## Mixins

* [`UUIDMixin`](/RFCs/backend/database/mixins.md#UUIDMixin)
* [`TimeDateMixin`](/RFCs/backend/database/mixins.md#TimeDateMixin)
* [`StatusMixin`](/RFCs/backend/database/mixins.md#StatusMixin)
* [`LangMixin`](/RFCs/backend/database/mixins.md#LangMixin)

## Fields

|       Field       |                             Type                             |                      Description                      |
| :---------------: | :----------------------------------------------------------: | :---------------------------------------------------: |
| `tutorial_anchor` | [`FK(TutorialAnchor)`](/RFCs/backend/database/tutorial_related_tables/tutorial/tutorial_anchor_table.md) |          The anchor point of this tutorial.           |
|     `authors`     | [`MTM(User)`](/RFCs/backend/database/user_system/user_table.md) |                  A list of authors.                   |
|      `title`      |                      `models.TextField`                      |       The title of this tutorial (translated).        |
|    `abstract`     |                      `models.TextField`                      |      The abstract of this tutorial (translated).      |
|   `content_md`    |                      `models.TextField`                      | The content of this tutorial in Markdown (translated) |
|  `content_html`   |                      `models.TextField`                      | The parsed html of the Markdown tutorial (translated) |

