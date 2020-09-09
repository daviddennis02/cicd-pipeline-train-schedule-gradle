# cicd-pipeline-train-schedule-gradle

This is a simple train schedule app written using nodejs. It is intended to be used as a sample application for a series of hands-on learning activities.

## Note: You must have Java JDK/JRE and Gradle installed on your machine/server to complete this lab

# Lab work
I implemented a build automation using Gradle on a nodejs application.
I made the following steps:

## 1. Your personal fork of the git repository is cloned to the cloud server
You need to clone your personal fork of the sample git repository to the cloud server. Make sure you perform the clone from your home directory.
You can do so like this:

```cd ~/```

```git clone git@github.com:<your username>/cicd-pipeline-train-schedule-gradle.git```

## 2. You initialized the project as a gradle project
Once you have cloned the git repo to your home directory, cd into the repo directory and then initialize the gradle build.

```cd ~/cicd-pipeline-train-schedule-gradle```

 ```./gradlew init```

## 3. Your gradle build generates a zip archive of the application in **dist/trainSchedule.zip**
The gradle build should generate an archive of the application in **dist/trainSchedule.zip**.
You can do this by adding a task to create this archive to build.gradle and ensuring the build task depends on it. Do this in the build.gradle file

```task zip(type: Zip) {

    ```from ('.') {
    
        include "*"
        
        include "bin/**"
        
        include "data/**"
        
        include "node_modules/**"
        
        include "public/**"
        
        include "routes/**"
        
        include "views/**"
        
    }
    destinationDir(file("dist"))
    baseName "trainSchedule"
}

build.dependsOn zip
zip.dependsOn npm_build
```

The full **build.gradle file** should look like this :

```plugins {
 id "com.moowork.node" version "1.2.0" 
}

node {
 download = true
}

task build

task zip(type: Zip) {
    from ('.') {
        include "*"
        include "bin/**"
        include "data/**"
        include "node_modules/**"
        include "public/**"
        include "routes/**"
        include "views/**"
    }
    destinationDir(file("dist"))
    baseName "trainSchedule"
}

build.dependsOn zip
zip.dependsOn npm_build
build.dependsOn npm_build
npm_build.dependsOn npmInstall
npm_build.dependsOn npm_test
npm_test.dependsOn npmInstall
```

Then, execute the gradle build to generate the archive:
``` ./gradlew build ```


## Running the app

It is not necessary to run this app locally in order to complete the learning activities, but if you wish to do so you will need a local installation of npm. Begin by installing the npm dependencies with:

    npm install

Then, you can run the app with:

    npm start

Once it is running, you can access it in a browser at [http://localhost:3000](http://localhost:3000)
