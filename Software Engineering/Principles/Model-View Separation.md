The **Model-View Separation principle** states that model (domain) objects should not have direct knowledge of view (presentation) objects, at least as view objects. So, for example, a Register or Sale object should not directly send a message to a GUI window object ProcessSaleFrame, asking it to display something, change color, close, and so forth.

A legitimate relaxation of this principle is the [[Observer]] pattern, where the domain objects send messages to UI objects viewed only in terms of an interface such as PropertyListener or AlarmListener.

A further part of this principle is that the domain classes encapsulate the information and behavior related to application logic. The window classes are relatively thin; they are responsible for input and output, and catching GUI events, but do not maintain data or directly provide application functionality.

The motivation for Model-View Separation includes: 
- To support cohesive model definitions that focus on the [[Dominio|domain]] processes, rather than on user interfaces.
- To allow separate development of the model and user interface [[Layers|layers]].
- To minimize the impact of [[Requerimientos|requirements]] changes in the interface upon the domain layer.
- To allow new views to be easily connected to an existing domain layer, without affecting the domain layer. 
- To allow multiple simultaneous views on the same model object, such as both a tabular and business chart view of sales information.
- To allow execution of the model layer independent of the user interface layer, such as in a message-processing or batch-mode system. 
- To allow easy porting of the model layer to another user interface [[Framework|framework]].

# "Upward" Communication
How can windows obtain information to display? Usually, it is sufficient for them to send messages to domain objects, querying for information which they then display in widgets—a polling or pull-from-above model of display updates.

However, a polling model is sometimes insufficient. For example, polling every second across thousands of objects to discover only one or two changes, which are then used to refresh a GUI display, is not efficient. In this case it is more efficient for the few changing domain objects to communicate with windows to cause a display update as the state of domain objects changes. Typical situations of this case include:
- Monitoring applications, such as telecommunications network management.
- Simulation applications which require visualization, such as aerodynamics modeling.

In these situations, a push-from-below model of display update is required. Because of the restriction of the Model-View Separation pattern, this leads to the need for "indirect" communication from lower objects up to windows—pushing up notification to update from below. There are two common solutions:
1. The [[Observer]] pattern, via making the GUI object simply appear as an object that implements an interface such as PropertyListener.
2. A Presentation [[Facade|facade]] object. That is, adding a facade within the Presentation layer that receives requests from below. This is an example of adding [[Indirección|Indirection]] to provide [[Variaciones protegidas|Protected Variation]] if the GUI changes.