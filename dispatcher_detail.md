**Dispatcher Overview**

### 1. **Definition**
A `Dispatcher` is a key component responsible for coordinating the process of matching conditions to actions, using regulations and aggregators. Dispatchers facilitate the rendering of templates by determining which actions to execute based on matching criteria.

### 2. **Components**
   - **Regulations Instance**: A collection of rules that determines the conditions for matches.
   - **Item_Aggregator Factory**: A factory that creates an aggregator for collecting matches related to individual items.
   - **Sequence_Aggregator Factory**: A factory that creates an aggregator for collecting matches for sequences of items.

### 3. **Dispatcher Types**
   - **Item Dispatcher**: Handles dispatching individual items using the `Item_Aggregator`.
   - **Sequence Dispatcher**: Handles dispatching sequences of items using the `Sequence_Aggregator`.

### 4. **Workflow**
   - The dispatcher receives either an item or a sequence.
   - It creates the appropriate aggregator using the relevant factory (`Item_Aggregator` or `Sequence_Aggregator`).
   - The aggregator collects matches from the regulations.
   - The dispatcher then executes the action(s) defined by the matched rule(s).

### 5. **Key Features**
   - **Flexible Aggregation**: Supports different types of aggregators, enabling flexibility in determining how many matches are used for action execution (e.g., first match, all matches).
   - **Mixed Rule Support**: Can work with regulations that consist of different types of rules, allowing for more dynamic and adaptable dispatch behavior.

### 6. **Use Cases**
   - **Template Rendering**: In template systems, dispatchers manage which actions or processing steps are applied to specific nodes or expressions.
   - **Conditional Processing**: Dispatchers are used to evaluate conditions and execute the appropriate logic, enabling more dynamic behavior within the framework.

### 7. **Extensibility**
Dispatchers are designed to be extended to support additional features, such as dispatching mappings or integrating more complex aggregators.

