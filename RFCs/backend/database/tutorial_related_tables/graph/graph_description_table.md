# `GraphDescription Table

The `GraphDescriptionBase` table is similar to [`TutorialTranslationBase`](/RFCs/backend/database/tutorial_related_tables/tutorial/tutorial_translation_base_table.md) and contains entries that describe what each graph is about.

## Mixins

* [`UUIDMixin`](/RFCs/backend/database/mixins.md#UUIDMixin)
* [`TimeDateMixin`](/RFCs/backend/database/mixins.md#TimeDateMixin)
* [`StatusMixin`](/RFCs/backend/database/mixins.md#StatusMixin)
* [`LangMixin`](/RFCs/backend/database/mixins.md#LangMixin)

## Fields

|     Fields     |                             Type                             |                 Description                 |
| :------------: | :----------------------------------------------------------: | :-----------------------------------------: |
| `graph_anchor` | [`FK(GraphAnchor)`](/RFCs/backend/database/tutorial_related_tables/graph/graph_anchor_table.md) | The graph associated with this translation. |
|   `authors`    | [`MTM(User)`](/RFCs/backend/database/user_system/user_table.md) |      The authors of this description.       |
|    `title`     |                      `models.TextField`                      |        The title of the description.        |
| `description`  |                      `models.TextField`                      |          The description content.           |
