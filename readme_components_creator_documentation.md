# JSON Structure Documentation

## Overview

This document describes the structure and relationships of the JSON file that defines UI components for an application. The JSON is designed to specify both static components and recyclable component templates for lists, facilitating the creation of dynamic interfaces.



## Main Keys

- **`theme_version`**: *(String)*  
  The version of the theme, e.g., `"1.0"`.

- **`published`**: *(String)*  
  The publication date of the theme in `YYYY-MM-DD` format, e.g., `"2024-01-01"`.

- **`data`**: *(Object)*  
  Contains the definitions of components divided into static components and recyclable templates.



## Data Structure

### `data`

The `data` object has two main sections:

1. **`components_statics`**: *(Object)*  
   Defines static UI components that are always present in the interface.

2. **`components_recycler`**: *(Object)*  
   Defines templates for components that will be used in recyclable lists (e.g., list items).



## Components Statics

### `components_statics`

An object where each key represents a group of static components. Each group includes:

- **`description`**: *(String)*  
  A textual description of the component group.

- **`components`**: *(Array)*  
  An array of component definitions detailing each component's properties.

#### Groups within `components_statics`:

1. **`mainmenu`**

   - **Description**: Group of components for the main menu.
   - **Components**:

     | Name                          | Type                   | Parent                         |
     |-||--|
     | `mainmenu_thumb`              | `HorizontalArrangement`| `main`                         |
     | `mainmenu_thumb_glow`         | `HorizontalArrangement`| `mainmenu_thumb`               |
     | `mainmenu_metadata_content`   | `VerticalArrangement`  | `mainmenu_thumb`               |
     | `mainmenu_metadata_title`     | `Label`                | `mainmenu_metadata_content`    |
     | `mainmenu_metadata_artist_name`| `Label`               | `mainmenu_metadata_content`    |

2. **`library_navigation_bar`**

   - **Description**: Library navigation bar.
   - **Components**: *(Empty array)*



## Components Recycler

### `components_recycler`

An object where each key represents a recyclable component template for use in lists. Each template includes:

- **`description`**: *(String)*  
  A textual description of the component template.

- **`components`**: *(Array)*  
  An array of component definitions detailing each component's properties.

#### Templates within `components_recycler`:

1. **`library_track_item`**

   - **Description**: Template for a library track item.
   - **Components**:

     | Name                    | Type                   | Parent                   |
     |-||--|
     | `library_track_content` | `HorizontalArrangement`| `main`                   |
     | `library_track_cover`   | `HorizontalArrangement`| `library_track_content`  |
     | `library_track_meta`    | `VerticalArrangement`  | `library_track_content`  |
     | `library_track_title`   | `Label`                | `library_track_meta`     |
     | `library_track_artist`  | `Label`                | `library_track_meta`     |
     | `library_track_menu`    | `HorizontalArrangement`| `library_track_content`  |

2. **`library_album_item`**

   - **Description**: Template for a library album item.
   - **Components**: *(Empty array)*



## Component Definitions

### Component Properties

Each component within the `components` arrays has the following properties:

- **`name`**: *(String)*  
  A unique identifier for the component.

- **`type`**: *(String)*  
  Specifies the type of the component (e.g., `Label`, `HorizontalArrangement`, `VerticalArrangement`).

- **`parent`**: *(String)*  
  The `name` of the parent component to establish hierarchy.

### Hierarchical Relationships

The `parent` property defines how components are nested within each other, creating a tree structure that represents the UI layout.

**Example from `mainmenu` components:**

- `mainmenu_thumb` is a child of `main`.
- `mainmenu_thumb_glow` and `mainmenu_metadata_content` are children of `mainmenu_thumb`.
- `mainmenu_metadata_title` and `mainmenu_metadata_artist_name` are children of `mainmenu_metadata_content`.



## Relationships and Hierarchy

- **Static Components** (`components_statics`):  
  These are always present in the UI and form the foundational structure.

- **Recyclable Components** (`components_recycler`):  
  Templates used to generate multiple instances of a component, such as list items in a dynamic list.

- **Parent-Child Relationships**:  
  The `parent` attribute establishes the nesting of components. A component's visual placement and behavior are influenced by its parent.



## Usage Notes

- **Component Names**:  
  Should be unique within their scope to prevent conflicts.

- **Empty Components Arrays**:  
  Groups or templates with empty `components` arrays are placeholders for future development.

- **Descriptions**:  
  Serve as inline documentation to clarify the purpose of each group or template.



## Summary

This JSON structure provides a clear and organized way to define UI components and their relationships. By separating static components from recyclable templates and explicitly defining parent-child relationships, it facilitates the dynamic generation of user interfaces in applications.



**Document Version**: Matches `theme_version` **1.0**  
**Last Updated**: Corresponds to `published` date **2024-01-01**


JSON Example:

{
    "theme_version": "1.0",
    "published": "2024-01-01",
    "data": {
      "components_statics": {
        "mainmenu": {
          "description": "Grupo de componentes para el menú principal",
          "components": [
            {
              "name": "mainmenu_thumb",
              "type": "HorizontalArrangement",
              "parent": "main"
            },
            {
              "name": "mainmenu_thumb_glow",
              "type": "HorizontalArrangement",
              "parent": "mainmenu_thumb"
            },
            {
              "name": "mainmenu_metadata_content",
              "type": "VerticalArrangement",
              "parent": "mainmenu_thumb"
            },
            {
              "name": "mainmenu_metadata_title",
              "type": "Label",
              "parent": "mainmenu_metadata_content"
            },
            {
              "name": "mainmenu_metadata_artist_name",
              "type": "Label",
              "parent": "mainmenu_metadata_content"
            }
          ]
        },
        "library_navigation_bar": {
          "description": "Barra de navegación de la biblioteca",
          "components": []
        }
      },
      "components_recycler": {
        "library_track_item": {
          "description": "Plantilla para un ítem de pista en la biblioteca",
          "components": [
            {
              "name": "library_track_content",
              "type": "HorizontalArrangement",
              "parent": "main"
            },
            {
              "name": "library_track_cover",
              "type": "HorizontalArrangement",
              "parent": "library_track_content"
            },
            {
              "name": "library_track_meta",
              "type": "VerticalArrangement",
              "parent": "library_track_content"
            },
            {
              "name": "library_track_title",
              "type": "Label",
              "parent": "library_track_meta"
            },
            {
              "name": "library_track_artist",
              "type": "Label",
              "parent": "library_track_meta"
            },
            {
              "name": "library_track_menu",
              "type": "HorizontalArrangement",
              "parent": "library_track_content"
            }
          ]
        },
        "library_album_item": {
          "description": "Plantilla para un ítem de álbum",
          "components": []
        }
      }
    }
  }
  