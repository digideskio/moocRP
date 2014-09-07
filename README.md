<img src="https://travis-ci.org/kk415kk/moocRP.svg?branch=master"/>
# moocRP: Reproducible Research Platform
Research platform for University of California, Berkeley researchers built by Kevin Kao in collaboration with Professor Zachary Pardos.

Built on Node.js server with Sails.js framework for an MVC architecture. Python/Bash scripts and D3 visualizations mixed in.

Releases will be numbered as ````< major version >.< minor version >.< patch number >````

## Current Release
0.1.1

## Author
Kevin Kao

## Table of Contents
* [Dependencies](#dependencies)
* [Setup Instructions](#setup-instructions)
* [Deployment](#deploying-to-production)
* [Visualization Instructions](documentation/visualizations.md)
* [Changelog](#changelog)
* [Features](#features)
* [Bugs](#bugs)
* [Roadmap](#roadmap)
* [License](#license)

## Dependencies

**Ubuntu Instructions**

* Install ````git````: ````sudo apt-get install git````
* Install Node.js ~0.10.25, minimum 0.10.x:

    ````
    sudo apt-get install python-software-properties
    sudo apt-add-repository ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get install nodejs
    ````

* Install npm (Node.js package manager) ~1.4.23:

    Use ````aptitude```` to install npm and downgrade Node.js through the prompt if conflicts occur.
    ````
    sudo apt-get aptitude
    sudo aptitude install npm 
    ````

* Install MySQL server: ````sudo apt-get install mysql-server-5.6````
* Install Sails.js ~0.10.4, minimum 0.10.x: ````sudo npm install -g sails````

## Setup Instructions
First, create a new folder called moocRP_base to clone this repository to:
````
mkdir moocRP_base
cd moocRP_base
git clone git@github.com:kk415kk/moocRP.git
````

After cloning this repository, run the setup script to create the correct directory structure. Enter in the correct MySQL user and password when prompted. This will create the database as well.
````
./bin/setup.sh
````

Once the setup script is run, the file structure setup should be in this format:
````
/moocRP_base
---- /moocRP (web application cloned from Github)
-------- /api
-------- /assets
------------ /scaffolds
------------ /visualizations
-------- ...
-------- /logs
-------- /bin
------------ setup.sh [setup script to create directory structure]
---- /datasets
-------- /non_pii
-------- /pii
-------- /extracted
-------- /encrypted
---- /visualizations
-------- /tmp
-------- /archives
````

Then, we need to install all npm package dependencies before launch:
````
sudo npm install
````

To launch the application, simply run:
````
sails lift
````

## Deploying to Production
Configure the production settings in your ````config/local.js```` file. Ensure that the port and env settings are correct.

To run the application in production continuously, we use the ````forever```` package:
````
forever start app.js --prod
````

## Visualization Upload Format
Note that all visualizations must use the field ````<%= dataset %>```` where they would normally pass in a text version of the dataset. There must be a ````main.html```` file inside the base of the uploaded archive that already has links to relevant scripts and additional files built into it.

## Changelog
0.1.1 - 08/14/2014: Patch to add support for future additions of datascrub types. UI browser compatibility updates, refactored database models to be more efficient.

0.1.0 - 08/11/2014: First minor version release.

0.0.3 - 07/01/2014: First version with working request/download system, visualization upload system, user management UI.

0.0.2a - 03/04/2014: Alpha version that replaced login system with Berkeley's CAS authentication.

0.0.1a - 02/01/2014: Alpha version with working login/verification system.

## Features
* SSL integration
* Node.js CAS client (login system)
* Secure dataset request and download system
* Visualization upload and approval system
* Administration controls
* UI theme
* Visualization to dataset hook
* GPG encryption system for dataset downloads

## Bugs
* When deploying in production, moocRP must be deployed once first in development mode so that the database tables are created - find a way to automate this.

## Roadmap
* Add "Reports" messaging system for managing bug handling/error messages
* Integrate JIRA ticketing system for open source release and collaboration
* Add support for hooking datasets to the visualization upload system
* Strip out CAS client to package into npm package
* Add profile updates for users
* Add support for sharing research papers
* Add support for running pre-processing scripts on datasets before visualizing (i.e. machine learning code)
* Investigate and implement automatic code review security
* Begin populating Github wiki for instructions on use
* Perform penetration testing and security checks
* Scale/stress testing + test suites need to be developed
* Add features to star/"bookmark" visualizations
* Implement alternative login system for non-CAS institutions

## License
MIT
