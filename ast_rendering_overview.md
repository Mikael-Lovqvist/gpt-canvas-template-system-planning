**AST Rendering Integration with Dispatchers**

### 1. **Overview**
This document outlines how the Abstract Syntax Tree (AST) is rendered using dispatchers, focusing on how rendering dispatchers differ from dumping dispatchers. It also discusses how different types of nodes, such as statements and inline expressions, are processed through rendering dispatchers.

### 2. **Rendering Dispatcher**
Rendering the AST involves dispatching nodes to convert them into rendered output. Unlike a dumping dispatcher that simply outputs the structure of the AST, a rendering dispatcher applies specific transformations and executes template logic to produce the final result.

- **Tree_View_Regex_Dispatcher**: A type dispatcher used to handle tree nodes, such as statements and inline expressions, during rendering. Different dispatchers are used to handle statements and inline expressions separately.
- **Rendering Flow**: Each type of node, such as a template statement (`§ include`) or an inline expression (`«current function»`), is dispatched to a specific handler responsible for rendering that part of the tree.

### 3. **Rendering Workflow**
   - **Step 1: Traversal**: The rendering process begins with a traversal of the AST. The `Rendering_Dispatcher` visits each node in the tree, determining whether it is a statement, an inline expression, or a text node.
   - **Step 2: Node Dispatch**: Depending on the type of node, it is dispatched using one of the dispatchers:
     - **Statement Dispatcher**: Handles nodes that represent template statements. For example, `§ include thing` might be dispatched to a handler that includes the contents of a file.
     - **Inline Dispatcher**: Handles inline expressions within a text node. For example, `«current function»` might be dispatched to a handler that replaces it with the current function's name.
     - **Text Node Handling**: If the node is a `Text_Tree`, the rendering dispatcher will render each part of the title. Inline expressions within the title are evaluated using the inline dispatcher, while string segments pass through unchanged.
   - **Step 3: Action Execution**: The corresponding handler executes an action to produce rendered output for that node. This could involve generating text, including content, or evaluating an expression.

**Example Rendering Flow**:
- A tree node containing `§ include thing` is dispatched to the statement dispatcher.
- The dispatcher matches the node using a `regex_rule` and calls the `handle_include` action, which renders the included content and adds it to the output.
- For a text node containing `pass # We will not do anything special in «current function»`, the inline dispatcher processes `«current function»`, replacing it with the actual function name during rendering, while other text segments pass through unchanged.

### 4. **Rendering vs. Dumping**
   - **Dumping Dispatcher**: Outputs the structure of the AST without executing any template logic. It is useful for debugging and understanding the structure of a template.
   - **Rendering Dispatcher**: Executes template logic, transforming the AST into the final output. This involves handling template statements, evaluating expressions, and including content as specified by the nodes.

### 5. **Rendering Dispatchers in Practice**
   - **Type Dispatcher**: A type dispatcher is used to differentiate between the different types of nodes—statements, inline expressions, and text nodes—and to apply the correct processing logic for each type.
   - **Tree-Level and Inline-Level Processing**: The rendering process uses separate dispatchers for tree-level and inline-level processing, ensuring that each type of content is handled appropriately and rendered accurately.

### 6. **Future Considerations**
   - **Optimizations**: As the rendering dispatcher evolves, optimizations can be applied to improve performance. For example, caching rendered content for reusable components or optimizing the traversal of the AST.
   - **Extensibility**: The rendering dispatcher is designed to be extended to support additional node types or more complex rendering logic, allowing for a flexible and adaptable rendering process.
   - **Handling Edge Cases**: While we currently focus on well-formed templates, future considerations should include identifying and handling edge cases, such as missing nodes or malformed structures. Validating templates before rendering will help ensure robustness and consistency in the rendering process.

### 7. **Summary**
The AST rendering process utilizes specialized dispatchers to transform nodes into rendered output. By using a combination of type dispatchers for statements, inline expressions, and text nodes, the rendering dispatcher ensures that each part of the template is processed correctly. This approach allows for both structured rendering and the execution of template logic, making it a powerful tool for generating dynamic content.

