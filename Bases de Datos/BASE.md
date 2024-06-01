_BASE_ stands for basically available, soft state, and eventually consistent. The acronym highlights that BASE is opposite of ACID, like their chemical equivalents.

#### ****_Basically available_****

_Basically available_ is the database’s concurrent accessibility by users at all times. One user doesn’t need to wait for others to finish the transaction before updating the record. For example, during a sudden surge in traffic on an ecommerce platform, the system may prioritize serving product listings and accepting orders. Even if there is a slight delay in updating inventory quantities, users continue to check out items.

#### ****_Soft state_****

_Soft state_ refers to the notion that data can have transient or temporary states that may change over time, even without external triggers or inputs. It describes the record’s transitional state when several applications update it simultaneously. The record’s value is eventually finalized only after all transactions complete. For example, if users edit a social media post, the change may not be visible to other users immediately. However, later on, the post updates by itself (reflecting the older change) even though no user triggered it.

#### ****_Eventually consistent_****

_Eventually consistent_ means the record will achieve consistency when all the concurrent updates have been completed. At this point, applications querying the record will see the same value. For example, consider a distributed document editing system where multiple users can simultaneously edit a document. If User A and User B both edit the same section of the document simultaneously, their local copies may temporarily differ until the changes are propagated and synchronized. However, over time, the system ensures eventual consistency by propagating and merging the changes made by different users.