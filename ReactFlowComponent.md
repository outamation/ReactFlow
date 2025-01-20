# ReactFlow Component Documentation

ReactFlow is a highly customizable library for building node-based editors, workflows, and interactive diagrams. This documentation covers all available props and their usage.

## Core Props

### Keyboard Configuration

- **deleteKeyCode**: If set, pressing the key or chord will delete any selected nodes and edges. Passing an array represents mutliple keys that can be pressed. For example, ["Delete", "Backspace"] will delete selected elements when either key is pressed.

- **selectionKeyCode**: If set, holding this key will let you click and drag to draw a selection box around multiple nodes and edges. Passing an array represents mutliple keys that can be pressed. For example, ["Shift", "Meta"] will allow you to draw a selection box when either key is pressed.

- **multiSelectionKeyCode**: 
  - Default: `"Control"`

- **zoomActivationKeyCode**: If a key is set, you can zoom the viewport while that key is held down even if panOnScroll is set to false. By setting this prop to null you can disable this functionality.
  - Default: `"Control"`

- **panActivationKeyCode**: If a key is set, you can pan the viewport while that key is held down even if panOnScroll is set to false. By setting this prop to null you can disable this functionality.
  - Default: `"Space"`

- **disableKeyboardA11y**: Disable keyboard accessibility features
  - Type: `boolean`
  - Default: `false`
    
### Customization

- **nodeTypes**: Object mapping of custom node types
  - Type: `{ [key: string]: React.ComponentType<NodeProps> }`
  - Default: `{}`

- **edgeTypes**: Object mapping of custom edge types
  - Type: `{ [key: string]: React.ComponentType<EdgeProps> }`
  - Default: `{}`

- **className**: Additional CSS classes for the wrapper div
  - Type: `string`
  - Default: `undefined`

### Event Handlers

#### Node Events

- **onNodeClick**: Fires when a node is clicked
  - Type: `(event: React.MouseEvent, node: Node) => void`

- **onNodeDragStart**: Fires when node dragging starts
  - Type: `(event: React.MouseEvent, node: Node, nodes: Node[]) => void`

- **onNodeDrag**: Fires while dragging a node
  - Type: `(event: React.MouseEvent, node: Node, nodes: Node[]) => void`

- **onNodeDragStop**: Fires when node dragging stops
  - Type: `(event: React.MouseEvent, node: Node, nodes: Node[]) => void`

- **onNodeMouseEnter**: Fires when mouse enters a node
  - Type: `(event: React.MouseEvent, node: Node) => void`

- **onNodeMouseMove**: Fires when mouse moves inside a node
  - Type: `(event: React.MouseEvent, node: Node) => void`

- **onNodeMouseLeave**: Fires when mouse leaves a node
  - Type: `(event: React.MouseEvent, node: Node) => void`

#### Edge Events

- **onEdgeClick**: Fires when an edge is clicked
  - Type: `(event: React.MouseEvent, edge: Edge) => void`

- **onEdgeMouseEnter**: Fires when mouse enters an edge
  - Type: `(event: React.MouseEvent, edge: Edge) => void`

- **onEdgeMouseMove**: Fires when mouse moves along an edge
  - Type: `(event: React.MouseEvent, edge: Edge) => void`

- **onEdgeMouseLeave**: Fires when mouse leaves an edge
  - Type: `(event: React.MouseEvent, edge: Edge) => void`

### Connection Handling

- **connectionMode**: Defines how connections can be drawn
  - Type: `ConnectionMode`
  - Values: `'strict' | 'loose'`
  - Default: `'strict'`

- **connectionLineType**: Style of the connection line while dragging
  - Type: `ConnectionLineType`
  - Values: `'bezier' | 'step' | 'smoothstep' | 'straight'`
  - Default: `'bezier'`

- **onConnect**: Fires when a new connection is created
  - Type: `(connection: Connection) => void`

- **onConnectStart**: Fires when a connection starts
  - Type: `(event: React.MouseEvent, node: Node) => void`

- **onConnectEnd**: Fires when a connection ends
  - Type: `(event: React.MouseEvent) => void`

### Viewport Controls

- **defaultViewport**: Initial viewport settings
  - Type: `Viewport`
  - Default: `{ x: 0, y: 0, zoom: 1 }`

- **minZoom**: Minimum zoom level
  - Type: `number`
  - Default: `0.5`

- **maxZoom**: Maximum zoom level
  - Type: `number`
  - Default: `2`

- **zoomOnScroll**: Enable zoom on scroll
  - Type: `boolean`
  - Default: `true`

- **zoomOnPinch**: Enable zoom on pinch gesture
  - Type: `boolean`
  - Default: `true`

### Panning Options

- **panOnScroll**: Enable panning while scrolling
  - Type: `boolean`
  - Default: `false`

- **panOnScrollSpeed**: Speed of panning while scrolling
  - Type: `number`
  - Default: `0.5`

- **panOnScrollMode**: Panning behavior mode
  - Type: `PanOnScrollMode`
  - Values: `'free' | 'vertical' | 'horizontal'`
  - Default: `'free'`

### Selection Options

- **selectionMode**: Defines how elements can be selected
  - Type: `SelectionMode`
  - Values: `'full' | 'partial'`
  - Default: `'full'`

- **selectionKeyCode**: Key used for selection
  - Type: `string`
  - Default: `'Shift'`

- **multiSelectionKeyCode**: Key used for multi-selection
  - Type: `string`
  - Default: `'Control'` (Windows) or `'Meta'` (MacOS)

### Element Behavior

- **nodesDraggable**: Allow nodes to be dragged
  - Type: `boolean`
  - Default: `true`

- **nodesConnectable**: Allow nodes to create connections
  - Type: `boolean`
  - Default: `true`

- **nodesFocusable**: Allow nodes to receive focus
  - Type: `boolean`
  - Default: `true`

- **edgesFocusable**: Allow edges to receive focus
  - Type: `boolean`
  - Default: `true`

- **edgesReconnectable**: Allow edges to be reconnected
  - Type: `boolean`
  - Default: `true`

### Performance Options

- **onlyRenderVisibleElements**: Only render elements visible in the viewport
  - Type: `boolean`
  - Default: `false`

### Styling

- **style**: Custom inline styles for the wrapper
  - Type: `React.CSSProperties`
  - Default: `undefined`

- **colorMode**: Color theme of the flow
  - Type: `'light' | 'dark'`
  - Default: `'light'`

### Dimensions

- **width**: Width of the component
  - Type: `number | string`
  - Default: `'100%'`

- **height**: Height of the component
  - Type: `number | string`
  - Default: `'100%'`

## Advanced Features

### Auto-Panning

- **autoPanOnConnect**: Enable auto-panning when connecting nodes
  - Type: `boolean`
  - Default: `undefined`

- **autoPanOnNodeDrag**: Enable auto-panning when dragging nodes
  - Type: `boolean`
  - Default: `undefined`

- **autoPanSpeed**: Speed of auto-panning
  - Type: `number`
  - Default: `undefined`

### Fit View

- **fitView**: Automatically fit the view to show all elements
  - Type: `boolean`
  - Default: `false`

- **fitViewOptions**: Options for the fit view behavior
  - Type: `FitViewOptions`
  - Default: `undefined`


### Debug

- **debug**: Enable debug mode for development
  - Type: `boolean`
  - Default: `false`
  - When debug mode is enabled (debug={true}), ReactFlow provides:
    - Visual indicators for node and edge interactions
    - Console logs for state changes and events
    - Performance metrics
    - Visual helpers for connection areas and bounds

## Usage Example

```jsx
import ReactFlow from 'reactflow';

const Flow = () => {
  const nodes = [
    { id: '1', type: 'input', position: { x: 0, y: 0 }, data: { label: 'Input' } },
    { id: '2', type: 'default', position: { x: 100, y: 100 }, data: { label: 'Default' } }
  ];

  const edges = [
    { id: 'e1-2', source: '1', target: '2' }
  ];

  return (
    <ReactFlow
      nodes={nodes}
      edges={edges}
      onNodesChange={onNodesChange}
      onEdgesChange={onEdgesChange}
      onConnect={onConnect}
      fitView
    />
  );
};

export default Flow;
```
