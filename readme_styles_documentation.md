# JSON Styles Documentation

## Overview

This document describes the structure and contents of the `styles.json` file, which defines styling properties for various UI components in the application. The styles are organized by component groups and states, allowing for dynamic theming and responsive design based on different conditions or user interactions.



## Main Structure

- **`styles`**: *(Object)*  
  The root object containing all style definitions, categorized by component groups.



## Component Groups

Within the `styles` object, styles are defined for different component groups. Each group corresponds to a set of components defined in the components JSON file and may have multiple states (e.g., `"default"`, `"playing"`, `"hide"`).

### Component Groups:

1. **`mainmenu`**

2. **`library_track_item`**

3. **`library_navigation_bar`**

4. **`library_album_item`**



## Structure Details

### 1. `mainmenu`

#### States:

- **`default`**:  
  Styles applied when the main menu is in its default state.

- **`hide`**:  
  Styles applied to hide or alter the visibility of components in the main menu.

#### Styles:

- **`default`**

  - **`mainmenu_thumb`**: *(Object)*  
    Styling properties for the `mainmenu_thumb` component.

    - **Properties**:
      - `"Height": 300`
      - `"PaddingBottom": 16`
      - `"MarginLeft": 110`
      - `"PaddingRight": 16`
      - `"PaddingTop": 16`
      - `"Visible": true`
      - `"Width": 350`

- **`hide`**

  - **`mainmenu_thumb`**: *(Object)*  
    Styling properties to hide the `mainmenu_thumb` component.

    - **Properties**:
      - `"Visible": false`

### 2. `library_track_item`

#### States:

- **`default`**:  
  Default styling for a library track item.

- **`playing`**:  
  Styling applied when a track is currently playing.

- **`downloading`**:  
  Styling applied when a track is downloading.

#### Styles:

- Currently, all state objects (`"default"`, `"playing"`, `"downloading"`) are empty `{}`. These are placeholders for future style definitions.

### 3. `library_navigation_bar`

#### States:

- **`default`**:  
  Default styling for the library navigation bar.

#### Styles:

- **`default`**: *(Object)*  
  Currently empty `{}`, indicating no styles have been defined yet.

### 4. `library_album_item`

#### States:

- **`default`**:  
  Default styling for a library album item.

#### Styles:

- **`default`**: *(Object)*  
  Currently empty `{}`, indicating no styles have been defined yet.



## Key Components and Properties

### Styling Properties Explanation

- **`Height`**: *(Number)*  
  The height of the component in pixels.

- **`Width`**: *(Number)*  
  The width of the component in pixels.

- **`PaddingBottom`**, **`PaddingTop`**, **`PaddingLeft`**, **`PaddingRight`**: *(Number)*  
  The padding inside the component borders.

- **`MarginLeft`**, **`MarginRight`**, **`MarginTop`**, **`MarginBottom`**: *(Number)*  
  The margin outside the component borders.

- **`Visible`**: *(Boolean)*  
  Determines whether the component is visible (`true`) or hidden (`false`).



## Usage Notes

- **States Management**:  
  Organizing styles by states allows dynamic styling changes based on user interactions or component statuses.

- **Empty Style Objects**:  
  Empty `{}` style objects are placeholders, indicating that styles can be added in the future as needed.

- **Component Group Consistency**:  
  The component groups in the styles JSON should correspond to those defined in the components JSON file to ensure styles are correctly applied.

- **Scalability**:  
  This structure allows for easy addition of new styles and states without disrupting existing configurations.



## Integration with Components

- **Applying Styles**:  
  When rendering components, the application should reference the styles defined in this JSON to apply the appropriate styling based on the component's group and current state.

- **State Changes**:  
  The application logic should handle state transitions (e.g., from `"default"` to `"playing"`) and update the component styles accordingly.



## Summary

The `styles.json` file provides a structured and flexible way to define the appearance of UI components across different states and conditions. By separating styles from component definitions, it enhances maintainability and allows for dynamic theming and responsive design within the application.



JSON Example:


{
  "theme_version": 1.0,
  "published": "2024-01-01",
  "styles": {
    "mainmenu": {
      "default": {
        "mainmenu_thumb": {
          "Height": 300,
          "PaddingBottom": 16,
          "MarginLeft": 110,
          "PaddingRight": 16,
          "PaddingTop": 16,
          "Visible": true,
          "Width": 350
        }
      },
      "hide": {
        "mainmenu_thumb": {
          "Visible": false
        }
      }
    },
    "library_track_item": {
      "default": {},
      "playing": {},
      "downloading": {}
    },
    "library_navigation_bar": {
      "default": {}
    },
    "library_album_item": {
      "default": {}
    }
  }
}