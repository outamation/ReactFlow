# React Flow Node Data Object Documentation

This documentation provides detailed information on the `data` object that can be used in React Flow to control the interactivity, styling, event handling, and other aspects of a node.

## 1. Node Interactivity

The following properties control how the node interacts with the user and the environment.

```js
data: {
  isSelectable: true,          // The node can be selected.
  isDraggable: true,           // The node can be moved.
  isConnectable: true,         // Connections can be made to/from this node.
  isResizable: true,           // The node can be resized.
  isZoomable: false,           // No zooming for this node.
  isClonable: true,            // The node can be cloned.
  isCollapsed: false,          // The node is not collapsed.
  canHaveMultipleLinks: true   // This node can have multiple connections.
}
```

## 2. Event Handlers
Event handlers define the actions that should be triggered based on user interactions with the node.
```js
data: {
  onClick: () => alert('Node clicked!'),                   // Triggered when node is clicked.
  onMouseEnter: () => console.log('Mouse entered node'),    // Triggered when mouse enters the node.
  onMouseLeave: () => console.log('Mouse left node'),       // Triggered when mouse leaves the node.
  onDoubleClick: () => console.log('Node double-clicked'),  // Triggered on double-click.
  onContextMenu: (e) => console.log('Right-click detected'), // Triggered on right-click.
  onDragStart: () => console.log('Drag started'),           // Triggered when drag starts.
  onDragStop: () => console.log('Drag stopped')             // Triggered when drag stops.
}
```
## 3. Custom Node Properties
Here, you store any custom properties that describe the node's state, category, label, or any unique metadata.
```js

  data: {
  label: 'Custom Node',         // The text label displayed on the node.
							OR
  label: (
        <>
          Node <strong>A</strong>				// we can provide a html tag in lable
        </>
      ),
  type: 'special-node',         // Custom type of the node.
  category: 'input',            // Category for organizing nodes.
  icon: '🔌',                   // Custom icon to represent the node.
  color: '#ff6347',             // Custom color for the node's background.
  customId: 'node-001',         // Unique ID for this specific node.
}
```
## 4. Custom Styling
These properties define the custom visual appearance of the node, such as color, font size, and padding.
```js

  data: {
  backgroundColor: '#ff6347',  // Custom background color.
  borderColor: 'blue',         // Custom border color.
  borderRadius: '12px',        // Rounded corners with 12px radius.
  fontSize: '16px',            // Font size for the text inside the node.
  padding: '10px',             // Padding inside the node.
  shadow: '0px 4px 6px rgba(0, 0, 0, 0.1)'  // Drop shadow for a subtle 3D effect.
}
```

## 5. Node State
Here, you can store the node's current dynamic state such as whether it's selected, active, or visible.
```js

  data: {
  isSelected: false,        // The node is not selected initially.
  isActive: true,           // The node is active.
  isVisible: true,          // The node is visible.
  isExpanded: false,        // Node is not expanded.
  isDisabled: false         // Node is not disabled.
}
```
## 6. Information for Node Behavior
This category handles the node’s relationships with other nodes or additional metadata that influences its behavior in the graph.
```js

  data: {
  linkedData: {            // Linked data related to the node.
    relatedNodeId: '3',    // The ID of a related node.
    relationship: 'parent-child'  // Defines a parent-child relationship.
  },
  parentId: 'parent-node-id',   // The parent node's ID (if applicable).
  connections: [            // Array of connections (edges) related to this node.
    { targetId: '2', sourceId: '1' },
    { targetId: '4', sourceId: '1' }
  ]
}
```
## 7. Custom Components
This is where you pass props or settings to custom components for rendering or behavior control.
```js

  data: {
  componentProps: {            // Custom props for a custom component.
    label: 'Custom Node',      // Label to pass to a custom node component.
    color: 'blue',             // Color passed to the custom component.
    icon: '🚀'                 // Icon to use in the custom component.
  },
  customRenderer: MyCustomRenderer  // Reference to a custom renderer function or component.
}

```
