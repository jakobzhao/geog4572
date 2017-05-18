# Course Project: Project Management

> Spring 2017 | Geography 472/572 | Geovisualization: Geovisual Analytics
>
> Instructor: Bo Zhao, zhao2@oregonstate.edu | Office Hours: 3-4pm T or by appointment @ strand 347
>
> TA: Kyle R. Hogrefe, hogrefek@oregonstate.edu| Office Hours: 1-2pm MF @ WLKN 257 and 2-4pm W @ WLKN 210


## Project Management Flows

**1\. Create a github repository**


![](img/make-readme-md-file.png)

When you create the repository, Please make sure **initialize the `README.MD`** file in the root directory.

**2\. Open the GitHub Page Support**

By this way, you can access the web pages in this repository as visiting a web site. The url address will be `http[s]://{your_account_name}.github.io/{your_git_repository}/{web_page_name.html}`.

![](img/github-page-support.png)

**3\. Add your team members**

To add your team members, you will firstly need to navigate through `Settings --> Collaborators` on your repository main page. Once added, all members can contribute to this project.

![](img/add-collaborators.png)

**4\. Update Repository**

You can update your repository by simply dragging and dropping your codes to the repository. However, it is tedious and not stable. Actually, Webstorm can help you easily update (`git pull & push`) your repository.

![](img/git-push-pull.png)

- Copy the git url. For example, the storymap's url is `https://github.com/jakobzhao/storymap.git`.

- Open the git url as a new project in Webstorm.

- Now you can add new files, modify existing files in Webstorm.

- To upload the local changes to the github server, navigate through `VCS --> Commit Changes ...`. Alternatively, you can press the **green arrow pointing upward** on the top menu bar.

- To download the latest version of the repository to your local computer, navigate through `VCS --> Update Project...`. Alternatively, you can press the **blue arrow pointing downward** on the top menu bar.

- When a team working on the same repository, all the members should be careful when upload the local chanegs. If there is a conflict, please carefully read through the conflict and merge them together.

**5\. Open Issues**

On your main page of github repository, please use the `Issues` tab to submit questions, fix bugs, and work on the wish list.

![](img/open-issues.png)

**6\. Download Bootstrap Template**

You can easily find a Bootstrap at [https://startbootstrap.com/](https://startbootstrap.com/). Here we will use the Morden Business Template at [https://startbootstrap.com/template-overviews/modern-business/](https://startbootstrap.com/template-overviews/modern-business/)

Or, you can download from [here](assets\startbootstrap-modern-business-gh-pages.zip).

![](img/modern-business.png)

Once downloaded, you can extract all the files and put them to the root directory of the repository on your local computer.

**7\. Web Map as the Index Page**

The index page is usually named after "index.html". For example, we can download the `nav bar` example of storymap and put it in the root directory.

> **Note:** debugging the http[s] conflict issue.

**8\. Make an About Page**

Link the about page in the nav bar by making a new `li` **element**.

> **Note:** Refer to [http://getbootstrap.com/components/](http://getbootstrap.com/components/) or [https://www.w3schools.com/bootstrap/default.asp](https://www.w3schools.com/bootstrap/default.asp), if you need to apply our Bootstrap widgets to your web based geovisualization.

**9\. Update your repository on github**

Uploading all your local changes to github by checking `Commit Changes...`. Then, Go to the repository mainpage to check whether the changes have been made or not..
