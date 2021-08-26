---
title: Install SonarQube on MacOSX

# Summary for listings and search engines
summary: Installation of SonarQube on MacOSX

# Link this post with a project
projects: []

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2018-06-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags: [SonarQube, MacOSX, brew, installation]


categories:
- How-to
---

## Steps:
0. Make sure you have `homebrew` installed in your machine, otherwise follow instrunctions at [brew.sh](https://brew.sh/).
1. Open terminal, run `brew install sonar`. Assuming brew installs SonarQube successfully, take a look at the last line of the terminal where the SonarQube location is printed. In my case it is `/usr/local/Cellar/sonarqube/7.1`.
2. Now run `brew install sonar-scanner` (N.B. sonar-runner is no longer available, it's replaced by sonar-scanner).
3. After installation is complete, run the following commands consecutively:
```
  export SONAR_HOME=/usr/local/Cellar/sonar-scanner/3.2.0.1227/libexec
  export SONAR=$SONAR_HOME/bin
  export PATH=$SONAR:$PATH
```
  [Note: exporting path in this way will work for the current session of terminal, for permanent use, I need to transfer these path variables to .bashrc file.]

4. Now we can run SonarQube from terminal by issuing this command `/usr/local/opt/sonarqube/bin/sonar console`.
5. Go to http://localhost:9000/ (or appropriate port based on your system) to view the main page of SonarQube. Use this credentials (username: admin, password: admin) to login.

References (a bit deprecated):
- [How to Setup SonarQube on Mac Part-1](http://zafercelaloglu.blogspot.com/2014/07/how-to-setup-sonar-on-mac-part-1.html)
- [Install Sonar Locally on OSX ](http://www.managerjs.com/blog/2015/11/install-sonar-locally-on-osx-and-analyze-a-javascript-project/)
