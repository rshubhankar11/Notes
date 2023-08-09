# Exception Handling Rules

1. A `try` block must be followed by either a `catch` block or a `finally` block.
2. A `catch` block must be preceded by either a `try` block or another `catch` block, with the `try` block at the top of the hierarchy.
3. A `catch` block can be followed by either another `catch` block or a `finally` block.
4. A `finally` block must be preceded by either a `try` block or a `catch` block, with the `try` block at the top of the hierarchy.
5. A `try` block can be followed by any number of `catch` blocks (zero or more).
6. A `try` block contains multiple `catch` blocks. If the exceptions specified in the `catch` blocks have an IS-A relationship, they must be specified in order from child to parent. If the exceptions don't have an IS-A relationship, they can be specified in any order.
7. A `try` block can contain at most one `finally` block.
8. Statements can be specified either before the blocks or after blocks or inside the blocks but not in between the blocks.
9. A `try` block may contain multiple `catch` blocks, but it can execute at most one `catch` block that matches the exception.

Remember that these rules guide how exception handling constructs can be organized in Java programs.
