# React Flow Documentation

React Flow is a powerful library for building node-based interfaces, such as workflows, flowcharts, and data visualizations. Below is a detailed guide covering its core concepts, features, and practical examples to help you get started.

---

## **1. Installation**

To install React Flow:

```bash
npm install @xyflow/react
```

```bash
yarn add @xyflow/react
```

Ensure your project is set up with React 16.8+ since React Flow requires hooks support.

---

## **2. Core Concepts**

### **Nodes**
- Nodes are the building blocks of React Flow.
- Each node represents an item in your flow and requires the following properties:
  - `id`: Unique identifier for the node.
  - `type`: Type of the node (e.g., input, output, or custom).
  - `position`: The position of the node on the canvas (using `x` and `y` coordinates).
  - `data`: Custom data that can be passed to the node component.

#### **Example Node**
```javascript
const node = {
  id: 'unique-id',
  position: { x: 100, y: 100 },
  data: { label: 'Node Label' },
  type: 'default', // optional, defaults to 'default'
  style: {}, // optional styling
  className: '', // optional CSS class
};
```

### **Edges**
- Edges connect nodes and represent the flow between them.
- Each edge has:
  - `id`: Unique identifier for the edge.
  - `source`: ID of the source node.
  - `target`: ID of the target node.
  - `label`: Used to provide lable on edge 
  - Optional properties like `type`, `animated`, or `label`.

#### **Example Edge**
```javascript
const edge = {
  id: 'edge-1',
  source: 'node-1',
  target: 'node-2',
  type: 'default', // optional
  animated: false, // optional
  label: 'Edge Label', // optional
  style: {}, // optional styling
};
```

### **Edge Types**
React Flow provides multiple edge types:
- `default`
- `straight`
- `step`
- `smoothstep`

You can also create custom edges for advanced visuals.

#### **Example of a Smoothstep Edge**
```javascript
const edge = {
  id: 'e1-2',
  source: '1',
  target: '2',
  type: 'smoothstep',
  label: 'Smooth Edge'
};
```
---

## **3. Getting Started**

### **Basic Setup**
To create a basic flow:

```jsx
import { ReactFlow, Controls, Background } from '@xyflow/react';
import '@xyflow/react/dist/style.css';
 
const edges = [
  { id: '1-2', source: '1', target: '2', label: 'to the', type: 'step' },
];
 
const nodes = [
  {id: '1', data: { label: 'Hello' },position: { x: 0, y: 0 },type: 'input'},
  {id: '2',data: { label: 'World' },position: { x: 100, y: 100 }},
];
 
function Flow() {
  return (
    <div style={{ height: '100%' }}>
      <ReactFlow nodes={nodes} edges={edges}>
        <Background />
        <Controls />
      </ReactFlow>
    </div>
  );
}
 
export default Flow;
```

### **Using ReactFlowProvider**
Wrap your application with `ReactFlowProvider` for advanced features like context sharing:

```jsx
import ReactFlow, { ReactFlowProvider } from "@xyflow/react";

const App = () => (
  <ReactFlowProvider>
    <ReactFlow elements={elements} />
  </ReactFlowProvider>
);
```

---

## **4. Features**

### **Custom Nodes**
You can define custom components for nodes by specifying a `nodeTypes` object:

#### **Custom Node Example**
```jsx
import { Handle, Position } from "@xyflow/react";

const CustomNode = ({ data }) => {
  return (
    <div className="custom-node">
      <Handle type="target" position={Position.Top} />
      <div className="custom-node-content">
        <h4>{data.title}</h4>
        <p>{data.content}</p>
      </div>
      <Handle type="source" position={Position.Bottom} />
    </div>
  );
};

// Registration
const nodeTypes = {
  customNode: CustomNode,
};

// Usage in ReactFlow
<ReactFlow nodeTypes={nodeTypes} />
```

### **Custome Node with multiple handles**
```jsx
import { useCallback } from 'react';
import { Handle, Position } from '@xyflow/react';
 
const handleStyle = { left: 10 };
 
function TextUpdaterNode({ data, isConnectable }) {
  const onChange = useCallback((evt) => {
    console.log(evt.target.value);
  }, []);
 
  return (
    <div className="text-updater-node">
      <Handle
        type="target"
        position={Position.Top}
        isConnectable={isConnectable}
      />
      <div>
        <label htmlFor="text">Text:</label>
        <input id="text" name="text" onChange={onChange} className="nodrag" />
      </div>
      <Handle
        type="source"
        position={Position.Bottom}
        id="a"
        style={handleStyle}
        isConnectable={isConnectable}
      />
      <Handle
        type="source"
        position={Position.Bottom}
        id="b"
        isConnectable={isConnectable}
      />
    </div>
  );
}
 
export default TextUpdaterNode;
```
- As you can see we added two source handles to the node so that it has two outputs. If you want to connect other nodes with these specific handles, the node id is not enough but you also need to pass the specific handle id. In this case one handle has the id "a" and the other one "b". Handle specific edges use the sourceHandle or targetHandle options that reference a handle within a node:

```jsx
const initialEdges = [
  { id: 'edge-1', source: 'node-1', sourceHandle: 'a', target: 'node-2' },
  { id: 'edge-2', source: 'node-1', sourceHandle: 'b', target: 'node-3' },
];
```

### **Adding Controls**
React Flow provides built-in controls for zooming and resetting:

```jsx
import { Controls } from 'react-flow-renderer';

<ReactFlow elements={elements}>
  <Controls />
</ReactFlow>;
```

### **Mini-Map**
Add a mini-map for better navigation:

```jsx
import { MiniMap } from 'react-flow-renderer';

<ReactFlow elements={elements}>
  <MiniMap />
</ReactFlow>;
```

---

## **5. Adding Interactivity**

- When you drag or select a node, the `onNodesChange` handler gets called. With help of the `applyNodeChanges` function you can then apply those changes to your current node state.

```jsx
import { useState, useCallback } from 'react';
import {
  ReactFlow,
  Controls,
  Background,
  applyNodeChanges,
  applyEdgeChanges,
} from '@xyflow/react';
import '@xyflow/react/dist/style.css';
 
function Flow() {
  const [nodes, setNodes] = useState(initialNodes);
  const [edges, setEdges] = useState(initialEdges);
 
  const onNodesChange = useCallback(
    (changes) => setNodes((nds) => applyNodeChanges(changes, nds)),
    [],
  );
  const onEdgesChange = useCallback(
    (changes) => setEdges((eds) => applyEdgeChanges(changes, eds)),
    [],
  );
 
  const onConnect = useCallback(
    (params) => setEdges((eds) => addEdge(params, eds)),
    [],
  );
 
  return (
    <div style={{ height: '100%' }}>
      <ReactFlow
        nodes={nodes}
        onNodesChange={onNodesChange}
        edges={edges}
        onEdgesChange={onEdgesChange}
        onConnect={onConnect}
        fitView
      >
        <Background />
        <Controls />
      </ReactFlow>
    </div>
  );
}
```

---

## **6. Advanced Features**

### **Dynamic Node and Edge Updates**
Add or remove nodes and edges dynamically:

```jsx
const addNode = () => {
  setNodes((nds) => [
    ...nds,
    { id: '4', data: { label: 'New Node' }, position: { x: 300, y: 300 } }
  ]);
};

const addEdge = () => {
  setEdges((eds) => [...eds, { id: 'e3-4', source: '3', target: '4' }]);
};
```

---

## **7. Events**

React Flow supports a variety of events for user interactions:

- `onNodeClick`: Triggered when a node is clicked.
- `onEdgeClick`: Triggered when an edge is clicked.
- `onLoad`: Provides the React Flow instance.

#### **Example: Logging Node Clicks**
```jsx
const onNodeClick = (event, node) => {
  console.log('Node clicked:', node);
};

<ReactFlow elements={elements} onNodeClick={onNodeClick} />;
```

---

This comprehensive documentation provides the foundational knowledge and examples to get started with React Flow. For additional use cases or specific queries, consult the official React Flow documentation or ask for guidance.

