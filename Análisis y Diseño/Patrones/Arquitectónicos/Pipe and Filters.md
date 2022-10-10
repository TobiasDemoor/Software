A pipeline consist of a chain of processing elements arranged so that the output of each element is the input of the next element. That's the definition.

![[AyD_Pipe_and_Filters.png]]

Conceptually, it should have a source to provide the initial data. And then step by step the data will be passed through filters over the pipes. And each filter supposes to transform the data provided and hand over the transformed data to the next filter through a pipe. Finally transformed data is handed over the final destination called "Sink" (the same message object is going to be used across the whole process).

Just assume that we have a requirement which can be broken into a series of tasks and,

1.  Let them run one after the other,
2.  Exists independently from each other
3.  Should be possible to add new tasks to chain or remove tasks from the chain by the time
4.  And should be possible to change the execution sequence with almost no effort