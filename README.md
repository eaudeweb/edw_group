# EDW group

Enable the group module to provide functionality for private tabs for a meeting.

## Prerequisites

Recommended patches for `group` module:

```php
"patches": {
    "drupal/entity_reference_revisions": {
      "#3364226 - Form error when no group admin role is automatically created": "https://www.drupal.org/files/issues/2023-08-02/group-form-error-3364226-12.patch",
      "#3104345 - Drupal\\group\\Plugin\\GroupContentEnablerBase::createAccess() must implement interface Drupal\\group\\Entity\\GroupInterface, null give": "https://git.drupalcode.org/project/group/-/merge_requests/86.patch",
      "#3397063 - Revisions tab appears twice on Groups": "https://www.drupal.org/files/issues/2023-12-12/group-revision-tabs-appear-twice-3397063-15.patch"
    }
}
```

Don't forget rebuilds the node access database: `node_access_rebuild(TRUE)`.

## Installation
1. Add the following snippet to the `repositories` section of your `composer.json` file:
```
{
    "type": "git",
    "url": "https://github.com/eaudeweb/edw_group.git"
},
{
      "type": "vcs",
      "url": "https://git.drupalcode.org/issue/node_access_grants-3494785"
}
```

2. Run
   ```composer require eaudeweb/edw_group:^1.0```

3. Enable the module:
   ``drush en edw_group``

## Architecture

Group types:
- `event` - Meeting group type used to create groups for meetings.

### Fields

| Field label | Field name  | Description                                                                 | Field type                    | Cardinality | Required | Translatable | Widget       |
|-------------|-------------|-----------------------------------------------------------------------------|-------------------------------|-------------|----------|--------------|--------------|
| Title       | title       | Build-in                                                                    | Text                          | Single      | Yes      | Yes          | Text field   |
| Meeting     | field_event | Automatically populated when an user with permissions create a new meeting. | Node entity reference (Event) | Single      | Yes      | No           | Autocomplete |

## Functionalities

The following functionalities are provided out of the box:

1. Group roles for Administrator and general users. If your website use another
role as administrator (such as System) you need manually add new role by at:
`/admin/group/types/manage/event/roles`.
2. Two new fields: `field_groups`and `field_moderator_groups`:
   - `field_moderator_groups` - Users in these groups have the permission to
   edit the meeting/section and its documents;
   - `field_groups` - groups that can view the specific section;
   Go to `/admin/structure/types/manage/{entity_type}/form-display` and display
   these fields in the edit form.
3. Two permissions.

## Other EDW modules:
* [edw_blocks](https://github.com/eaudeweb/edw_blocks)
* [edw_decoupled](https://github.com/eaudeweb/edw_decoupled)
* [edw_demo_data](https://github.com/eaudeweb/edw_demo_data)
* [edw_document](https://github.com/eaudeweb/edw_document)
* [edw_event](https://github.com/eaudeweb/edw_event)
* [edw_media](https://github.com/eaudeweb/edw_media)
* [edw_paragraphs](https://github.com/eaudeweb/edw_paragraphs)
* [edw_person](https://github.com/eaudeweb/edw_person)
* [edw_project](https://github.com/eaudeweb/edw_project)
* [edw_themes](https://github.com/eaudeweb/edw_themes)
* [edw_utilities](https://github.com/eaudeweb/edw_utilities)