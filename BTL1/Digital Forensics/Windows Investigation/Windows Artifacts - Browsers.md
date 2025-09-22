This lesson will focus on artifacts that can be gathered from internet browsers. These can be a goldmine for information relevant to a digital forensic investigation, such as websites that have been visited when they were last visited, what the user did on the websites, files that have been downloaded, search form strings, autofill usernames and password, and lots more. We will be looking at the three most popular web browsers on Windows: **Microsoft Edge, Google Chrome, and Mozilla Firefox.** The artifacts we will be looking at are:

- **Cookies**
- **Favorites**
- **Downloaded Files**
- **URLs Visited**
- **Searches**
- **Cached Webpage**
- **Cached Images**

We will be using:

- **KAPE –** [Download](https://www.kroll.com/en/insights/publications/cyber/kroll-artifact-parser-extractor-kape)
- **Browser History Viewer –** [Download](https://www.foxtonforensics.com/browser-history-viewer/) (Choose the 100% free version)
- **Browser History Capturer –** [Download](https://www.foxtonforensics.com/browser-history-capturer/)
## Acquisition via KAPE

We have already covered KAPE in **DF3) Digital Evidence Collection** – but for this lesson, we’re going to utilize the browser-based modules to collect information from a running system, retrieving data from Chrome, Edge, and Firefox. Feel free to download KAPE and follow along, analyzing your own systems browser files!

To start, let’s load up KAPE and select our target directory and output directory. We’ll be analyzing our host system’s C drive, with an output destination as `**/Desktop/KAPE Browser Forensics**`.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7aeb56acf5d182eadc985f2a93ee84cffff15e6fdc49834fbd6fab3c3661cf5e2166ca227a6106a0aee263fae77c.png)

Next, we need to select browser-based Targets, so we can collect the files we need to perform browser forensics. We’re going to enable the Targets for Chrome, Firefox, and Edge.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/86fd20b0d23a3dce3f3740db925b46db879000e3e155198bf010166e2f791f873c58af3a3065856c0f800e79b90b.png)![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/853dee97f608ff6fd08c5ef69c95cb9a55b0f3b5df521b088e2190f4479347b0d57076e01c6af9be4610704c7442.png)![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e152803c6ea10414967d0428713ab6dd7508dbe354b283a92f57f87f4fe3c9a6a1f2a6c915223b31a2d36ead21ca.png)

That’s it – we can now run KAPE by clicking on “Execute!” in the bottom right corner. KAPE took 52 seconds to gather all the information we requested. Opening our defined output folder we can see the files we retrieved.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a932aa152efad7ed622e5a393b1e3f24e8424bf0a7f2027edc784ce5e23ac20862e6b11844c0113f4134633c2d68.png)

We can find lots of interesting Google Chrome files at the following file path: `KAPE Browser Forensics\C\Users\JBeam\AppData\Local\Google\Chrome\User Data`
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/549eee1a21b58cd9cae639ee6f963b5dd4c1fc74df350b4c6b9bda8e3b85af14f560a9d43b75ff62671eb9708618.png)

We can also find interesting Firefox files at the following file path (please note we haven’t used Firefox much on this PC, so there’s limited data to display compared to Edge/Chrome): `KAPE Browser Forensics\C\Users\JBeam\AppData\Roaming\Mozilla\Firefox\Profiles`
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f17be76ee55945979b5c5a0ead02f76f12b4b811f5a3e2b04f3e5511056d6b5d6b9327c821041a9e5710bc24dec9.png)

The best way for you to get a feel of browser forensics is to try it out on your own system (or if you don’t run Windows as your host OS, create a Windows VM, spend a day browsing the web inside it, then complete the actions we’ve done above to analyze your browsing activity!). We highly suggest that students grab their own browser files via KAPE and take some time to mess around looking at what has been retrieved, and analyzing their own files.

---
## Browser History Viewer

There’s another way we can retrieve browser information, using two tools: Browser History Capturer (BHC) and Browser History Viewer (BHV), free tools developed by Foxton Forensics. We can run Browser History Viewer on its own, but if you’re running it on the system you’re investigating, it will fail at trying to retrieve Microsoft Edge files, even if it is run with elevated admin privileges. That’s where Browser History Capturer comes in, we can forcefully retrieve all important files for browser forensics, and then import it into BHV. These tools allow us to view a huge amount of browsing history, when sites were accessed, visit counts, cached webpages, and cached images. If you want to follow along, download the tools, and analyze your own system!

First, let’s run Browser History Capturer to collect all the files we need. We need to select the User Profile we want to collect data on. The Browsers and Data tickboxes will be toggled on by default, so we can leave them as they are. The destination by default will be a new directory named “Capture” within the BHC folder. We can alter this or leave it as it is – for this example we won’t alter the destination location. Now we can click on Capture.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8e25f0b2ae65ef409e53c29d4e83abc2a6a2d8bdf66ebd745a0ee987ff962dde318605e3cab156238d26bc1f5f48.png)

We can now see a folder named “Capture” in our BHC directory.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a71e58260c591bff1328fe850bc4e041968e3e4eecfff7d2c6c57ec1ffe7aef784ea169241a178a4fa616150bef6.png)

Next we need to import this directory into Browser History Viewer. Open BHV and go to **File** > **Load History**. Select “Load history captured using the Browser History Capturer tool” and navigate to the “Capture” directory we just created using BHC. Then click Load.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/83d7777b2f9dcf80fcdc5d3cdcb8fc644c5e4d4ab351f513a118f182bbf6e6def9f220f08a0e4439231aa409e51b.png)

Now that we’ve imported the data, let’s go through the different panes that Browser History Viewer has. We have split it into three regions.

- **Pane 1 –** This is where the information imported is displayed, with three tabs: Website History, Cached Images, and Cached Web Pages. On the default tab Website History we can see the dates when sites were visited, the titles of the site if available, the full URL, visit counts, and the browser used to access the web resources.
- **Pane 2 –** Website Visit Count, showing how many resources have been accessed per month.
- **Pane 3 –** Filter Pane, allowing us to filter by keywords (such as website names), filter by date, or filter by web browser.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1f0756c615728b22461e1f613e2af4552b3529ecf8f475e1f283f6fbd711ce8c1bfc62a0d2481ec54d728a780b88.png)

Let’s filter on web resources that have been accessed via the Chrome browser by selecting Chrome from the dropdown list in Pane 3. In the below screenshot you can see it’s mainly us slaving away on the Blue Team Level 1 course! We can see when we visited certain webpages, how many times we’ve visited them, and that this activity occurred in the Chrome browser.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/bef7dd3d3c3e68a658c3b857dc5ce9ccfa9df73e76c9edda6c33a3cab52e9a091e03aab2578b26939e13839ea9d9.png)

Next let’s take a look at the Cached Images tab of Pane 1. Below is a screenshot that shows us navigating between different pages, which shows the URLs of images, and displays them where Pane 2 was previously. These are typically downloaded from adverts, but can also indicate user browsing activity.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fecbf1b6e8e393337a74179514461a4637b3d628d8d1346676847eb526fa8fdc1f326291d1c94e8e1afc52f91e72.gif)

And finally, let’s take a look at the third tab of Pane 1, Cached Web Pages. This tab allows us to view webpages that have been downloaded to the system to speed up loading time. In the below screenshot we have selected a web request on 08/06/2020 at 17:40, which is a Google search for “linkedin security blue team”. In the bottom pane we can visually see the screen that the user would’ve viewed when performing this search.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8d9daec69d347107d94fb8cb7e14da2052d82b7e8688806b571c27f383458006326d5b1db299606e0494fa03c43c.png)

If you haven’t already, we highly suggest you play around analyzing your own system to view browsing history, cached images, and cached web pages using KAPE, and Browser History Capturer and Browser History Viewer.