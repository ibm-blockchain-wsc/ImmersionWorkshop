# Immunichain Guided Tour

# What is Immunichain?

Immunichain is the tracking of immunization records of a child on the
blockchain. The participants in the network include: a guardian, a
medical provider and a member organization (think of summer camp or a
high school athletic department). Between these participants, we are
granting or revoking access to the child's immunization record. If you
are a medical provider and have access to the child's immunization
record, you can administor new immunizations. Additionally, if you are a
member, you can view the child's immunization record if you have access
to it. Why would we grant access for a member to our child's
immunization record? Well, for example, each summer millions of kids go
to summer camp. Tradtionally, each summer camp needs to verify that the
child has had all their shots. In today's world, the guardian or the
doctor has to fill out a form explaining that the child has had all
their immunization shots. In tomorrow's world, we can utilize
blockchain to not only stop having to fill out paper forms of maybe
incorrect information, but we can simply allow the member to view the
records and - once approved - we can revoke their access so that they
don't keep the child's information.

# How did Immunichain Come About?

Immunichain came from an IBM internal Blockchain hackathon in May of
2017. Around the same time, an Open Mainframe Project intern Kevin Lee
from University of Illinois at Urbana-Champaign was tasked to use this
use case to make a blockchain application. He ended up making this
application that you are going to use today.

The use case is a true story for on of our co-workers, as her grandson
lived in 3 different countries before coming to the US. Transferring her
grandson's medical records took a very long time due to the
complications of the US law and information the other 3 countries were
providing. While the medical records were being transferred, her
grandson ended up having the same immunization shots multiple times -
which can be harmful to the child. They finally were able to get the
medical record transferred to a US doctor and the child is doing well
today. While the original intent of this use case was for children, you
can think of doing a similar use case with pets and their shot records.

# What are you going to accomplish today?

Today, you will take a guided tour of the Immunichain UI. This UI will
allow you to create a guardian, medical provider and a member
organization. Once you have a guardian you can create a child (it's
that simple...) and grant access to your medical provider and member
organzations. Based on whether or not you have granted access or revoked
access, the participants will be able to administor new immunization
shots or read the child's immunization record. Underneath this UI, is
the blockchain network doing all the work for you through REST API
calls. If you took this to your friend, they should not even know that
blockchain is doing all the work underneath the covers. In a real world
application, Immunichain would be split up into 3 different UI's
comprised of our 3 participants.

# Pre-Requisites for Mac

-   Web Browser (Chrome preferably)
-   Internet connectively

# Pre-Requisites for Microsoft

-   Web Browser (Chrome preferably)
-   Internet connectively

# Author

-   Austin Grice
