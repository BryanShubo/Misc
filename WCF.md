A session is a correlation of all messages sent between two endpoints. Instancing refers to controlling the lifetime of user-defined service objects and their related InstanceContext objects. Concurrency is the term given to the control of the number of threads executing in an InstanceContext at the same time.

PerCall: A new InstanceContext (and therefore service object) is created for each client request.
PerSession: A new InstanceContext (and therefore service object) is created for each new client session and maintained for the lifetime of that session (this requires a binding that supports sessions).
Single: A single InstanceContext (and therefore service object) handles all client requests for the lifetime of the application.


Transactions provide a way to group a set of actions or operations into a single indivisible unit of execution. A transaction is a collection of operations with the following properties:

Atomicity. This ensures that either all of the updates completed under a specific transaction are committed and made durable or they are all aborted and rolled back to their previous state.

Consistency. This guarantees that the changes made under a transaction represent a transformation from one consistent state to another. For example, a transaction that transfers money from a checking account to a savings account does not change the amount of money in the overall bank account.

Isolation. This prevents a transaction from observing uncommitted changes belonging to other concurrent transactions. Isolation provides an abstraction of concurrency while ensuring one transaction cannot have an unexpected impact on the execution of another transaction.

Durability. This means that once committed, updates to managed resources (such as a database record) will be persistent in the face of failures.
