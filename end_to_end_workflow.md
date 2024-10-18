**Dispatcher Overview**

### 1. **Definition**
A `Dispatcher` is a key component responsible for coordinating the process of matching conditions to actions, using regulations and aggregators. Dispatchers facilitate the rendering of templates by determining which actions to execute based on matching criteria.

### 2. **Components**
   - **Regulations Instance**: A collection of rules that determines the conditions for matches.
   - **Item_Aggregator Factory**: A factory that creates an aggregator for collecting matches related to individual items.
   - **Sequence_Aggregator Factory**: A factory that creates an aggregator for collecting matches for sequences of items.
   - **State Management**: Dispatchers utilize `State_Manager` to handle the lifecycle of the aggregation process, managing states like `Pending`, `Working`, `Aborted`, and `Finished`.

### 3. **Dispatcher Types**
   - **Item Dispatcher**: Handles dispatching individual items using the `Item_Aggregator`.
   - **Sequence Dispatcher**: Handles dispatching sequences of items using the `Sequence_Aggregator`.

### 4. **Workflow**
   - The dispatcher receives either an item or a sequence.
   - It creates the appropriate aggregator using the relevant factory (`Item_Aggregator` or `Sequence_Aggregator`).
   - The aggregator collects matches from the regulations.
   - The dispatcher then executes the action(s) defined by the matched rule(s).

**Example Workflow**:
- In the macro system, the `Tree_View_Regex_Dispatcher` is used to match tree nodes against specific patterns. For example, the pattern `§ include thing` is matched and processed by `handle_include`, which creates an instance of `MAST.Include`.
- Inline expressions, such as `«current function»`, are handled by `Inline_Macro_Processor` using a `Regex_Transformer`. This shows how dispatchers manage both tree-level and inline patterns effectively.

### 5. **State Management**
   - **States**: The dispatcher and aggregators work together to manage states during the dispatching process:
     - **Pending**: Initial state where no work has been performed.
     - **Working**: Actively processing items and aggregating results.
     - **Aborted**: The dispatch or aggregation process has been halted, typically due to an error.
     - **Finished**: The process is complete, and all necessary actions have been executed.
   - **State Transitions**: State transitions are controlled by the `State_Manager` using predefined rules, ensuring proper coordination between dispatching and aggregation.

### 6. **Key Features**
   - **Flexible Aggregation**: Supports different types of aggregators, enabling flexibility in determining how many matches are used for action execution (e.g., first match, all matches).
   - **Mixed Rule Support**: Can work with regulations that consist of different types of rules, allowing for more dynamic and adaptable dispatch behavior.

### 7. **Use Cases**
   - **Template Rendering**: In template systems, dispatchers manage which actions or processing steps are applied to specific nodes or expressions.
     - **Macro System Example**: The macro system uses `Tree_View_Regex_Dispatcher` to parse and process templates, allowing for dynamic content generation and transformation.
   - **Conditional Processing**: Dispatchers are used to evaluate conditions and execute the appropriate logic, enabling more dynamic behavior within the framework.

### 8. **Extensibility**
Dispatchers are designed to be extended to support additional features, such as dispatching mappings or integrating more complex aggregators. The use of state management makes the dispatcher reliable in concurrent environments and provides control over its lifecycle.

