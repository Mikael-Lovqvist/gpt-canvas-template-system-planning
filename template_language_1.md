**Template Language 1 Specification**

### 1. **Overview**
Template Language 1 is designed to represent text as a hierarchical structure, using indentation to define relationships between nodes, similar to languages like Python or YAML. The language will be processed by the generic template processor, with support for both fixed content and template-specific statements.

### 2. **Text Structure**
   - **Text Tree**: Text is represented as a tree defined by its indentation level. Nodes have titles and optional bodies.
   - **ABC.Text.Text_Tree**: The `ABC.Text.Text_Tree` structure is used to represent each text node, consisting of:
     - **Title**: The label of the node.
     - **Body**: The nested nodes that fall under the current node.

**Example**:
```
root
    branch1
        leaf1
    leaf2
```
- In this example, there are four nodes: `root`, `branch1`, `leaf1`, and `leaf2`.
- The body of `root` consists of the nodes `branch1` and `leaf2`.

### 3. **Node Types and Processing Rules**
   - **Template Statements**: If a `Text_Node` title begins with `§`, it is treated as a template statement. The body of this node will be processed as part of the template logic.
   - **Fixed Content**: Nodes whose titles do not begin with `§` are considered fixed content of the template.
     - **Inline Expressions**: Within fixed content nodes, anything wrapped in `«` and `»` is treated as a template inline expression.
   - **Indentation**: Indentation is used to determine the parent-child relationships between nodes.
   - **Processing Template Statements**: Nodes beginning with `§` are processed as template logic, allowing for dynamic content generation.
   - **Inline Expressions**: Inline expressions enclosed in `«` and `»` are evaluated as part of the template rendering process, replacing them with the computed values.

### 4. **Escape Sequences**
Escape sequences are used to include special characters within the content:
   - `\«` → `«`
   - `\»` → `»`
   - `\xNN` → Unicode character `N` (8-bit hex)
   - `\uUUUU` → Unicode character `U` (16-bit hex)
   - `\\` → `\`

These escape sequences allow for flexibility in writing templates, especially when using reserved characters within content.

### 5. **Future Considerations**
Additional escape codes or node types may be introduced in the future to extend functionality, but the current focus is on providing the basic set needed for initial template processing.

