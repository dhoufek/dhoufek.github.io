Part of using the UNL Web Framework is ensuring that the files necessary to render the page and the global interface and interactions (commonly referred to as framework/template dependents) are kept up to date with the latest released standards. This ensures that your UNL Web Framework-based website will have the latest fixes and Web Developer Network member contributions. Great care has gone into the framework to minimize the number of files that need to be kept in sync. Historically, the entire package of global HTML, CSS and JavaScript needed to be maintained and synchronized on all web servers that were not part of the university’s central hosting provider (Frontier then, UNL CMS now). This was done for a number of reasons – including technical limitations of the central hosting provider – and to allow other web server administrators to deploy the framework without a run-time dependency on a server outside of their control. Unfortunately, this kind of deployment led to significant fragmentation of released versions and caused problems for server administrators who utilized servers which had to be restarted after changes to these static files.

Thanks to advances in our hosting infrastructure, we now generally recommend that all site owners make use of the `fixed.dwt` type framework template. It includes instructions to load most static resources from our distribution servers on UNL CMS. These servers have full support for HTTPS, so that technical limitation has been removed. For the static files that we have not yet been able to incorporate into the framework from a central location, [synchronization](https://github.com/unl/wdntemplates/wiki/Synchronizing-the-Framework#synchronizing-the-files) is still **required** for all web servers hosting pages in the UNL Web Framework.

Server administrators who would like to continue using the old synchronization pattern (having a copy of all files necessary to render the page) may do so by following the `local.dwt` type framework template that only has references to files relative to the root of your website domain. We generally discourage this kind of deployment unless there is a strong and well articulated reason for not using the centralized hosting provider for these framework dependents. Please note, that the requirement for [synchronization](https://github.com/unl/wdntemplates/wiki/Synchronizing-the-Framework#synchronizing-the-files) _remains_; and it becomes a little more complicated as you must have infrastructure that is capable of building the framework dependents with instructions to only pull static files from your fully-synchronized server. Simply doing a full sync from the central hosting provider (`cms.unl.edu` or `www.unl.edu`) will result in a some files being loaded from your domain and others from the central hosting provider, as the central hosting provider only provides the template dependents that have been built to use the central hosting provider’s domain for loading extra, asynchronous dependencies. Instructions for building the framework dependents are included in the [README file](https://github.com/unl/wdntemplates/#building-template-resources) that accompanies the source code. If you do not fully understand what is being discussed in this paragraph, you should avoid having to maintain a web server and consider migrating your website to [UNL CMS](https://cms.unl.edu/).

# Release Schedule
* New framework releases happen the first Tuesday of every month.
* Release candidates are deployed to the staging server (`unlcms-staging.unl.edu`) one week before the release (the last Tuesday of the month before).
* Occasionally, there will need to be a hotfix deployed outside of this schedule. An email will be sent to the Web Developer Network mailing list in this case.
* Check out and subscribe to our [Release Calendar](https://events.unl.edu/wdn_release/upcoming/).

# Synchronizing the Files
There are two types of synchronization you may follow to successfully deploy the framework to your own web server, (A) [minimal](https://wdn.unl.edu/#minimal-synchronization) or (B) [full](https://wdn.unl.edu/#full-synchronization-build). Brief instructions for these types of synchronization are below. You are recommended to follow one of these synchronization processes in an automated fashion such as a cron (Unix) or scheduled task (Windows). We recommend that this automated process run every night, or at least within a day of the release being announced through one of the feeds mentioned above.

## Minimal Synchronization
Currently the minimal synchronization type requires that you download and host the static HTML files that are a part of every framework page. These are the files that ensure the framework header and footer have the most up-to-date global content and that your pages load the proper version of the framework CSS and JavaScript. These static HTML files should be hosted in a location that your template files are aware of, by default this is the `/wdn/` root domain directory. The file you download will contain this `wdn` directory. Please use caution when copying/merging this directory into your production environment, as you may need to keep historical files or directories in your server’s `wdn` directory from previous iterations of the framework. At this time the `templates_5.3` is the only directory included in this synchronization package. 

[Download Minimal Synchronization Package](https://wdn.unl.edu/downloads/wdn_includes.zip)

An example command line (shell) script for downloading this file and deploying it to the web server’s root directory located at `/var/www/html` using the `curl`, `unzip`, and `rsync` Unix utilities is provided below.
```
#!/bin/sh
curl -L https://wdn.unl.edu/downloads/wdn_includes.zip -o wdn_includes.zip
unzip wdn_includes.zip
rsync -a wdn /var/www/html
rm wdn_includes.zip
rm -r wdn
```

## Full Synchronization/Build
A full synchronization or build will copy all static files necessary to run a completely self-contained version of the framework on your server. These static files should be hosted in a location that your template files are aware of, by default this is the `/wdn/` root domain directory.

[Download pre-built files from UNL CMS](http://wdn.unl.edu/downloads/wdn.zip)

[Download source files from GitHub](https://github.com/unl/wdntemplates/archive/master.zip)

An example command line (shell) script for downloading the pre-build files (built to load additional resources from UNL CMS) and deploying it to the web server's root directory located at `/var/www/html` using the `curl`, `unzip`, and `rsync` Unix utilities is provided below.
```
#!/bin/sh
curl -L https://wdn.unl.edu/downloads/wdn.zip -o wdn.zip
unzip wdn.zip
rsync -a wdn /var/www/html
rm wdn.zip
rm -r wdn
```

An example command line (shell) script for downloading the source files, building the static files for your server, and deploying it to the web server’s root directory located at `/var/www/html` using the `curl`, `unzip`, and `rsync` Unix utilities is provided below. This script assumes you already have the necessary utilities for building the framework installed (`git` and `node`).
```
#!/bin/sh
curl -L https://github.com/unl/wdntemplates/archive/master.zip -o wdntemplates-master.zip
unzip wdntemplates-master.zip
cd wdntemplates-master
make dist
cp downloads/wdn.zip ../wdn.zip
cd ..
rm wdntemplates-master.zip
rm -r wdntemplates-master
unzip wdn.zip
rsync -a wdn /var/www/html
rm wdn.zip
rm -r wdn
```

## Historical Synchronization
Our central hosting provider maintains a historical listing of the previous 3.0, 3.1, 4.0, 4.1, 5.0, 5.1, 5.2 and 5.3 releases. Currently, you can view a directory listing of these files at https://www.unl.edu/wdn/. A Unix utility like `wget` could be used to fully synchronize with this historical listing. However, we do not recommend this kind of synchronization anymore.

An example command line command for downloading the historical, pre-build files (built to load additional resources from UNL CMS) and deploying them to the web server’s root directory located at `/var/www/html` using the `wget` Unix utility is provided below.
```
wget -rq -nH -np -l 15 --cut-dirs=1 --reject "index.html*,*.LCK" http://www.unl.edu/wdn/ -P /var/www/html/wdn/
```

## Automation Techniques
We leave the automation process as an exercise for your web server administrator. Depending on your server environment we recommend the following tools for automating the scripts above: [cron](https://linux.die.net/man/5/crontab) (Linux), [launchd](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html) (macOS), [Scheduled Task](https://docs.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page) (Windows). For Windows environments, please be aware that the scripts above have been written for unix environments and they may require adjustments to work with the Windows command prompt or Powershell utilities.