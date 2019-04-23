Immunichain Guided Tour
=======================

**What is Immunichain?**

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

**How did Immunichain Come About?**

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

**What are you going to accomplish today?**

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

**Pre-Requisites for Mac**

-   Web Browser (Chrome preferably)
-   Internet connectively

**Pre-Requisites for Microsoft**

-   Web Browser (Chrome preferably)
-   Internet connectively

Part 1: Create your Participants & Child
========================================

**1.**  Begin by going to the Immunichain UI below:

    https://immunichain.zcloud.marist.edu/login/

**2.**  Click on `Create an account`

**3.**  You will be prompted to fill out a profile for your participant. In
    the `Role` field, select your participant (Guardian, Healthcare
    Provider and Member Organization). Based on your role, fill out the
    rest of the information.

**NOTE:** You will want to make your profile specific to you. As
everyone is creating their participant, it is being inserted into one
database. By the time you create your participants, there could be
multiple medical providers and member organizations. If you make them
specific to you, you will know which medical provider and member
organiation to assign to your child.

Here is my guardian:

![image](images/immunichainimages/1.png)

**4.**  Once you have successfully created a guardian, you will be welcomed
    with the guardian's homepage

![image](images/immunichainimages/2.png)

**5.**  Once you have looked through the available options for our guardian,
    you can click on `logout` in the top right
    
**6.**  Once you are on the Immunichain homepage, you can click on
    `Create an account` once more. This time, make a healthcare provider

Here is my healthcare provider:

![image](images/immunichainimages/3.png)

**7.**  Once you have made your healthcare provider, you will be graced with
    its profile

![image](images/immunichainimages/4.png)

**8.**  Once you have looked through the available options for our
    healthcare provider, you can click on `logout` in the top right
    
**9.**  Once you are on the Immunichain homepage, you can click on
    `Create an account` once more. This time, make a member organization

Here is my member organization:

![image](images/immunichainimages/5.png)

**10.** Once you have made you member organization, you will be greeted with
    its profile

![image](images/immunichainimages/6.png)

**11.** Look through the available options for our member organization. Once
    you are finished, you can click on `logout` in the top right

Part 2: Create a Child and Grant Access
=======================================

**1.**  You should be on the Immunichain homepage. If you are log into your
    `guardian`

![image](images/immunichainimages/7.png)

**2.**  Once you get to your guardian's profile, scroll down and click on
    `Continue` of `Add a Child`
    
**3.**  Fill out the information for our hypothetical child and choose the
    healthcare provider and member organization that you created

**NOTE** Remember how I said - at the beginning - that there would be
multiple healthcare providers and members to choose from, you now know
why I said to make the participants specific to you.

![image](images/immunichainimages/8.png)

**4.**  Click on `Submit` once you have filled out your child\'s information

![image](images/immunichainimages/9.png)

**5.**  Click on `return home` and that should take you back to the
    guardian's profile. Now that you think you have create a child, you
    can confirm by click on `Continue` of `View Record`
    
**6.**  Select our new child and click on `Continue`

**7.**  You should now see all the information you just filled in for our
    child

![image](images/immunichainimages/10.png)

**8.**  You will notice that we have already granted access for our
    healthcare provider, Suzie, and then our member organization,
    KennysCamp.

If you did not grant access for our other participants when creating the
child, you will see blank information in the `Medical Providers` and
`Member Organizations` section. You can change that by going to the
guardian's profile and then click on `Authorize Member` or
`Add Medical Provider`

Part 3: Add Immunizations
=========================

**1.**  Navigate your way back to the Immunichain homepage. Once you are
    there, log into our member organization

![image](images/immunichainimages/11.png)

**2.**  Click on `Continue` of the `View Record` tile

**3.**  You should only see the children in which we have access to - in
    this case, it should only be `BabyDennis`

![image](images/immunichainimages/12.png)

**4.**  Click on `Continue` and you should see all of Dennis's information

![image](images/immunichainimages/13.png)

**5.**  You will notice, that there are no immunization shots on Dennis\'s
    record. Let's change that. We can do that by logging out of our
    Member and then logging into our Healthcare Provider

![image](images/immunichainimages/14.png)

**6.**  Once you get to the medical providers homepage, click on `Continue`
    of `Add Immunization`. Then select our child, `Dennis`.
    
**7.**  You should now be on the screen to add immunizations for Dennis. Go
    ahead and give Dennis an immunization shot with today's date

![image](images/immunichainimages/15.png)

**8.**  Go ahead and click on `Submit` to add this immunization shot. Once
    you have done that, you will should see a `Success` message

![image](images/immunichainimages/16.png)

**9.**  Now that we have successfully added an immunization shot, we can see
    if our member can see it on their end. You can do that by logging
    out of the healthcare provider and then logging into our member.
    
**10.** Once you are on the member's profile, you can click on `Continue`
    of the `View Record` tile and selecting Dennis.
    
**11.** Now that we have selected Dennis, you can see see the updated
    information of Dennis's immunization shot

![image](images/immunichainimages/17.png)

**12.** Imagine if you were a SummerCamp or another member participant that
    needs childrens medical shot record. Doing this digital increases
    the accuracy of the data due to the healthcare provider inputting
    the data right when the shot was administered. Additionally, this
    will allow them to increase their efficency of approving children
    into their camp, for example.

Now if you were a guardian and a summer camp already approved your
child, we would want to revoke that member from seeing our child\'s
immunization record. How do we do that? We will do exactly that in the
next section.

Part 4: Revoking Access
=======================

**1.**  Navigate back to Immunchain's homepage and log into the Guardian\'s
    profile
    
**2.**  Click on `Continue` of the `Deauthorize Member` tile

**3.**  Select Dennis as our child and then select our Member, KennysCamp,
    as the one we revoking access to

![image](images/immunichainimages/18.png)

**4.**  You should get a `Success` message once click on `Submit` of the
    revoking our member

![image](images/immunichainimages/19.png)

**5.**  Now, log out of our guardian and log into our medical provider

**6.**  Once in the medical provider's profile, click on `Continue` of the
    `Add Immunization` tile
    
**7.**  Select our child, Dennis, and then add another immunization to his
    record

![image](images/immunichainimages/20.png)

**8.**  Once you get the `Success` message, click on `Back to Home`.

**9.**  You should still be in the guardian's profile. Since you are, click
    on `Continue` of the `View Record` tile. Then select our child,
    Dennis. You should then see Dennis's updated immunization record

![image](images/immunichainimages/21.png)

**10.** Log out of our medical provider and then log into our member,
    KennysCamp.
    
**11.** Click on `Continue` of the `View Record` tile. You should see the
    message of: `You do not have any children`. This means the
    KennysCamp can't view Dennis's immunization record anymore.

![image](images/immunichainimages/22.png)

Optional: If you want to grant KennysCamp as a member again, you can go
back into the guardian's profile. Once there, you can click on
`Continue` of the `Authorize Member` tile. Then you can grant KennysCamp
as an authorized member for Dennis. Now if you go back to KennysCamp,
click on `Continue` of the `View Record` tile and you should see the
updated information for Dennis.

![image](images/immunichainimages/23.png)

**End of Lab**

Summary
=======

In this guided lab of Immunichain, you created 3 different participants:
a guardian, a medical provider and a member. Then having created a
guardian, we create a child. Using our child, Dennis, we added
immunization shots and showed that from the members perspective. Knowing
that our member could see the immunization record, we revoked their
access to the medical record. We did that by going to the guardian
perspective and deauthorizing the member. To reconfirm that we revoked
the member's access to the immunization record, we went back to our
member and saw the message saying that we `Don't have any children`
meaning that KennysCamp wasn't authorized to see anyone's medical
record.

Moving forward, what ways do you think you could improve this blockchain
network? How would insurance effect this network? What missing componets
do you think would benefit this network?
