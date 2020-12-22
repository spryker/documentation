[Spryker Jarvis](https://github.com/spryker/jarvis) is the command-line tool that allows you to analyze your Spryker-based project and eventually migrate it to the most up-to-date version of Spryker. The tool helps you to quickly get answers to the following questions:

*     How outdated is your project compared to the latest Spryker product release?
*     What features does your project already use, and what are the other features it could use?
*     What should you do to update your project to the latest Spryker product release?
*     How did the new Spryker module version affect your project?
*     How far are your modules behind the latest Spryker minor and major module versions?
*     What features are compatible with your current project version?

Spryker Jarvis is meant mostly for developers working on the Spryker projects who want to get a clear view of what it takes to update their project to the latest product release version of Spryker. The tools can also be useful for project managers, as it answers the question “How outdated is the project?“ and helps to estimate efforts to update the project.

This article will teach you how to install and use the Spryker Jarvis tool for analysis and upgrade of your project.

## Prerequisites
Before you can install Spryker Jarvis, make sure that you have:

* [Spryker project installed locally.](https://documentation.spryker.com/docs/dev-getting-started#step-1--install-spryker)
* [NodeJS installed.](https://nodejs.org/en/download)  

## Installation
To install Spryker Jarvis:

1. Fork/Clone/Download [Spryker Jarvis repository](https://github.com/spryker/jarvis).
2. Open the terminal and do the following:
    2.1. Go to the Spryker Jarvis folder.
    2.2. Run `npm install`.

That’s it. Now you have Spryker Jarvis installed.

## Usage
To migrate your project to the latest version of Spryker using the Spryker Jarvis tool:

Inside the Spryker Jarvis folder, run `node jarvis.js <path to your spryker project folder>`.

Follow the terminal script about your project name.

Open `http://localhost:7777` in your browser and enjoy the migration analysis.

## Jarvis views
Depending on your project’s specifics and your goals, you can use various migration views available in Jarvis and take necessary actions. There are three views:

* *Basic* view - for migrating to a newer product release.
* *No-features* view - for upgrading your project modules to their current major and minor versions.
* *Missing-features* view - for upgrading your project with the compatible Spryker features.

### Basic view: Migrating to a newer product release
To migrate to a newer product release, use the Jarvis *basic* view. This view lists all the Spryker features that require an upgrade to make your project up-to-date with the latest Spryker version. For each feature, the upgraded and the removed dependencies are listed.

This view is especially useful when: 

* You have a Spryker-based product and finished the main development part of it.
* Your project uses feature repositories, or the project is based on the Spyker[ B2B Demo Shop](https://documentation.spryker.com/docs/b2b-suite) or the [B2C Demo Shop](https://documentation.spryker.com/docs/b2c-suite). 

Use this view if you want to stay up-to-date with Spryker and get new features every Spryker product release.

To see this view, run `node jarvis.js <path to your spryker project folder>` in the terminal. This shows you the main Spryker Jarvis page with information about the product release you can upgrade your project to.
![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Migrating+Your+Project+to+the+Latest+Spryker+Version+with+Spryker+Jarvis/Screenshot+2020-08-04a+at+13.58.50.png){height="" width=""}

It can be that a dependency has been upgraded, but no migration is needed. In this case, we will highlight it:
![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Migrating+Your+Project+to+the+Latest+Spryker+Version+with+Spryker+Jarvis/Screenshot+2020-08-04+at+14.00.13.png){height="428" width="312"}

In this view, under the list of features to upgrade and the dependencies, you can also check the features you don’t use but might be interested in. The recently released features are marked as *New feature*:

![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Migrating+Your+Project+to+the+Latest+Spryker+Version+with+Spryker+Jarvis/unused-features.png){height="" width=""}

 You can go to the repository of each feature by clicking the feature names. 

### Upgrading Modules to their Current Majors

Run `node jarvis.js <path to your spryker project folder> --no-features` in the terminal to see this view.

This view is only useful when your project does not use Spryker features, as it lists just modules.

![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Migrating+Your+Project+to+the+Latest+Spryker+Version+with+Spryker+Jarvis/Screenshot+2020-08-06+at+09.57.56.png){height="" width=""}

This view allows you to understand to what extent your project is outdated. You can see all modules that are behind majors and minors.

By clicking a module, you will see its detailed view as shown in the video below.

<video width="720" height="480" controls>
  <source src="https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Migrating+Your+Project+to+the+Latest+Spryker+Version+with+Spryker+Jarvis/Screen+Recording+2020-08-06+at+10.04.06.mov">
</video>

The detailed view allows you to migrate your modules to the latest version of their current majors. You can also see the changes between your current version and the latest version of the next major.

### Upgrading your Project with the Compatible Spryker Features
Run `node jarvis.js <path to your spryker project folder> --missing-features` in the terminal to see this view.

This view is useful when you want to use Spryker features but do not know which versions are compatible with your project.

![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Migrating+Your+Project+to+the+Latest+Spryker+Version+with+Spryker+Jarvis/Screenshot+2020-08-06+at+10.42.15.png){height="" width=""}

This view allows you to see all Spryker features that are compatible with your project and which minimum version you must take.

Here you can also see what modules are already installed on your project and what are missing. To install the missing modules, follow the [integration guide](https://documentation.spryker.com/docs/about-integration) of the respective feature.

<video width="720" height="480" controls>
  <source src="https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Migrating+Your+Project+to+the+Latest+Spryker+Version+with+Spryker+Jarvis/Screen+Recording+2020-08-06+at+10.50.47.mov">
</video>

Most of the time, you will need to add missing dependencies to your project to be able to use the Spryker features. But in some cases, you can swap your modules with the Spryker features, because your project already has all the dependencies:

![image](https://spryker.s3.eu-central-1.amazonaws.com/docs/Developer+Guide/Migrating+Your+Project+to+the+Latest+Spryker+Version+with+Spryker+Jarvis/Screenshot+2020-08-06+at+11.02.11.png){height="" width=""}

## Reference
Check out the [How to use Spryker Jarvis video](https://training.spryker.com/pages/spryker-tv?wchannelid=papy2tx2f6&wmediaid=jtkjogkxht) to see Spryker Jarvis in action.

