# hr-workflow
# 🛠️ HR Workflow Designer Prototype (React + React Flow)

This prototype implements a mini-HR Workflow Designer module as specified in the Tredence assignment.

The application is built with **React, Vite, Tailwind CSS, and React Flow**.

## 🚀 How to Run

1.  **Clone the repository.**
2.  **Install dependencies:**
    ```bash
    npm install
    ```
3.  **Start the development server:**
    ```bash
    npm run dev
    ```
4.  Open your browser to the local address provided (usually `http://localhost:5173`).

## [cite_start]🧱 Architecture and Design Choices [cite: 101]

[cite_start]The architecture prioritizes modularity, clear separation of concerns, and extensibility[cite: 6, 82, 80].

### [cite_start]1. Folder Structure [cite: 79]
* [cite_start]**`src/components/nodes/`**: Houses all custom node UIs (`StartNode`, `TaskNode`, etc.). They are abstracted via `BaseNode.jsx` for consistent styling and handle placement.
* **`src/components/panels/`**: Contains side-panels: `PropertiesPanel` for node configuration and `SandboxPanel` for testing. [cite_start]This separates the graph state logic from the UI configuration logic[cite: 80].
* [cite_start]**`src/api/`**: Contains `mockApi.js`, an abstraction layer for all async calls, fulfilling the mock API requirement[cite: 60].

### [cite_start]2. Complex Form Handling (Properties Panel) [cite: 35, 84]
The `PropertiesPanel` is highly dynamic:
* It reads the `selectedNode.type` to render only the relevant fields (e.g., `Approver Role` for `ApprovalNode`, but `Assignee` for `TaskNode`).
* [cite_start]It handles controlled components, directly updating the `data` payload of the selected React Flow node via the `setNodes` function from the canvas[cite: 58].
* [cite_start]For the `AutomatedStepNode`, it fetches action definitions from the mock API and dynamically renders action parameters based on the chosen action, demonstrating dynamic form generation[cite: 54].

### [cite_start]3. Mock API Interaction [cite: 60, 61, 16]
* [cite_start]**`/automations`**: Fetches a static list of actions (e.g., `send_email`) that populates the dropdown in the `AutomatedStepNode` configuration form[cite: 62, 53].
* [cite_start]**`/simulate`**: Accepts the full workflow JSON (`nodes` and `edges`) [cite: 69] [cite_start]and runs a mock, step-by-step traversal, returning a detailed log to the `SandboxPanel`[cite: 74].

### [cite_start]4. Workflow Simulation (Sandbox Panel) [cite: 70, 76]
[cite_start]The `SandboxPanel` demonstrates graph serialization [cite: 72] and state reasoning:
* It serializes the current `nodes` and `edges` state.
* [cite_start]The `mockApi.simulateWorkflow` function performs basic validation (e.g., checks for a **Start Node** [cite: 34]) and simulates a sequential execution, logging each step and displaying it to the user.

## ✅ Completed Deliverables

* [cite_start]React application (Vite) 
* [cite_start]React Flow canvas with multiple custom nodes (Start, Task, Approval, Automated, End) [cite: 14, 23-28]
* [cite_start]Node configuration/editing forms for each type [cite: 15, 35-57]
* [cite_start]Mock API integration (`/automations` and `/simulate`) [cite: 16, 60]
* [cite_start]Workflow Test/Sandbox panel [cite: 17, 70]
* [cite_start]README explaining architecture and design choices [cite: 18, 103]

## 💡 What I Would Add With More Time

* [cite_start]**Graph Validation**: Implement proper cycle detection and unconnected component checks before simulation (currently, basic Start Node check is done)[cite: 75].
* [cite_start]**Custom Hooks**: Use a custom hook (e.g., `useNodeConfig`) to centralize the form state logic and further simplify the `PropertiesPanel`[cite: 81].
* [cite_start]**Visual Validation Errors**: Display errors (e.g., missing fields) visually on the canvas nodes themselves[cite: 93].
* [cite_start]**Undo/Redo**: Implement `undo/redo` functionality, typically using a state management library like Zustand or Redux for tracking history[cite: 91].
