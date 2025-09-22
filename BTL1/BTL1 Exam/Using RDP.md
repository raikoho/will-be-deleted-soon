Similar to how SSH works, RDP is a method for connecting from one Windows-based system to another providing a graphical user interface. Below is a short guide on how to connect from one Windows system to another using RDP. You will be using this method in the exam to access other systems, so ensure that you are familiar with using it to prevent losing time in the exam.

Before we can connect to another system using RDP, we need the following information:

- **Remote system IP address**
- **Valid username**
- **Valid password**

Once you open RDP via a shortcut or from the Windows search bar, the following window will appear:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a32e133a191f381d1ede6a77c99d83752c9717d3122606fc11678b5f4c8771920a97a73b434b381d6a508c5b22b7.png)

One interesting thing we can do with RDP is create a link between a hard drive on our local system so that it can be accessed from the remote system. This is great for pulling files back to our system for later analysis. To do this, first click on ‘Show Options’ at the bottom of the Window. Next click on the ‘Local Resources’ tab and click the ‘More…’ button at the bottom.


![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0d66453392b8352328092cf455ad13c9c3cfe0248ca0df3ad2bebd5ae3488ee11bd8bc17fdcf127aace673423f36.png)

If you expand the Drives section we can toggle the C: drive, which means it will now be available through our RDP session!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/754fda9a1c42856310925d7f7fe3c8395e3db07a2a85205eb25ee9e1c2a1aa3e7f2e2f85a5aadb8b2a1d986beb74.png)

Once we initiate the connection, it’ll look as if you’re actually on the system itself! The only difference is the toolbar at the top of the Window.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/af52ed73ee0c33dcc278f72ed7a74126f28148c9932cf500faf5072c6384aa955057a962e4a39008a9ffbabcea3d.png)

As mentioned before, we have mapped our local C: drive, so let’s head over to This PC to confirm we can access it.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3f7f272512940c57a3dcffabb5ad27fa916f41b503690fcaa41a4bae1a76795d370731c904f91f0490380317a69e.png)

We can see the local drives on the remote system at the top, then down at the bottom of the window we have the C: drive on our local system. We can now copy files from the remote system to that drive, and then access them once we close the RDP session!

To end this RDP session, all we need to do is click the ‘X’ on the toolbar in the top middle of the screen. You can also click the ‘-’ to minimize the session, just like any other program window.