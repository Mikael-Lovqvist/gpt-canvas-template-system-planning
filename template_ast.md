**Template Language Abstract Syntax Tree (AST)**

### 1. **Overview**
The Template Language AST provides a structure to represent template languages, including Template Language 1 and others that may be developed in the future. The AST is designed to encapsulate the core elements of a template language in a generic way, enabling flexibility and reuse across different template implementations.

### 2. **Template_Text_Tree**
   - **Structure**: The `Template_Text_Tree` is similar to the `Text_Tree`, but with additional capabilities to handle template-specific constructs.
     - **Title**: The title of the `Template_Text_Tree` is not just a string. It is represented as a sequence that can contain:
       - **Strings**: Simple text segments.
       - **Template_Inline_Expression Instances**: Expressions that will be dynamically evaluated during template processing.
     - **Body**: The body contains the nested nodes of the current `Template_Text_Tree` instance, similar to the `Text_Tree` structure.

**Example**:
```
root
    branch1
        §template_statement
    «inline_expression»
```
- In this example, the `root` node contains `branch1` and an inline expression node.
- The `branch1` node has a template statement (`§template_statement`) as part of its body.

### 3. **AST Node Types**
   - **Template_Text_Tree**: Represents the overall tree structure of a template, similar to `Text_Tree`, but adapted for template processing.
     - **Title**: A sequence that can contain strings and `Template_Inline_Expression` instances.
     - **Body**: Represents child nodes, which may be other `Template_Text_Tree` nodes.
   - **Template_Inline_Expression**: Represents an inline expression that will be evaluated during the template rendering process.

### 4. **Interface Requirements**
   - **Common Root with Text_Tree**: The `Template_Text_Tree` must share a common interface root with `Text_Tree`. This ensures consistency across different types of text trees and enables them to be treated uniformly by components of the framework that need to handle both.
   - **Shared Properties**:
     - **Title and Body**: Both `Template_Text_Tree` and `Text_Tree` must have `title` and `body` properties.
     - **Traversal Methods**: Methods to traverse nodes, allowing the framework to process the tree structure regardless of whether it is a template or a basic text tree.

### 5. **Extending the AST**
The Template Language AST is designed to be extensible, allowing additional node types or properties to be introduced as new template languages or features are developed. The goal is to keep the core structure consistent while allowing flexibility in the specific capabilities of different template languages.

