# Visual Tooling on the Web With Che Workspaces

## Overview
This project aims to enable existing desktop based visual tooling written with the Eclipse Rich Client Platform to be usable from a web browser with zero installation and managed as part of an Eclipse Che workspace, bringing the advantages of portable, containerised, collaborative , zero deployment , cloud based workspaces to existing tried and tested applications traditionaly run on the desktop.

## Background
Software Development is changing. 

Since a while now IDE’s are no longer just for coding by programmers in languages with high learning curves. Domain specific Languages and visual tooling have developed to lower the barrier for domain experts who are not programmers to express their expertise and ideas effectively using technology.

Also as development moves from laptops and desktops into servers and containers in the cloud, new alternatives to traditional software development workflow have emerged, lowering the barrier for domain experts to collaborate, and making things more efficient for technical teams.

Do we still need to install and upgrade IDE’s on our laptops/desktops, or manage parallel development and releases with technical tools separate from our organisations issue management systems, or walk to our colleagues desk to do some joint development or review, or follow complex setup to hopefully get something identical to our colleague running on our machine? No, we don’t.

In this new world of cloud based development and collaboration, should we throw away our stable visual tools or upgrade them to make use of new this new cloud based tech? What if we can bring all the wonders of cloud based collaboration to our existing visual tooling? 

This project aims to allow us to bring existing stable visual tooling to the world of zero installation, access from anywhere, collaborate and share without barriers, cloud based approach. 

## The Tech
We aim in this project to allow eclipse based IDE’s (specifically Rich Client Platform applications) to make use of eclipse Che as a Workspace server to provide cloud based collaboration and management of tooling, while using Apache Guacamole to make these traditionally desktop applications easy to use in a web browser with zero installation.

So we are mixing 3 open source projects, Eclipse Che workspace server, Eclipse based IDE’s, and Apache Guacamole.

Apache Guacamole is a service which allows remotely viewing applications in web browsers.

We build upon an existing proof of concept by Rich Lucente at Redhat  which integrates the eclipse based JBoss Developer Studio with Apache Guacamole and Openshift (https://github.com/rlucente-se-jboss/jbds-via-html5), and we expand on that to add the concept of cloud managed workspace that comes from eclipse Che.

As an example eclipse based, desktop based, RCP application we are using Obeo designer which is an a compact packaging of the components required to run Eclipse Sirius graphical modelling IDE.

Eclipse Che is sometimes considered as a web based IDE, however it is more accurate to call it a workspace server, where each workspace is a container (or group of containers) that provides everything needed for a workspace... one of these things a workspace often requires is an IDE. Currently Che provides a Javascript Orion based IDE 'injected' into a workspace, what if the IDE associated with a workspace was 'simply' a small client that allows web access to the running RCP/eclipse based application using apache guacamole? This could allow the Eclipse Che front end to be used to provision/stop/start/snapshot/share/persist these containers.

In Eclipse Che, projects (i.e. project files) are mounted into the workspace, so that they are available both inside of the workspace and also available on long term storage, this can help us manage the persistence lifecycle of files in our containerized RCP apps.

For those who prefer their web user interfaces to be more web-native interfaces such as Javascript/HTML5/GWT then using this approach to get all the goodness of Che's workspace server for existing application could be used as a stepping stone into cloud based development while work on web native user interfaces is happening in the background.

## The goal
The first goal is to get a working demo with Obeo designer running in the cloud as containerised eclipse che workspaces, and managed by the eclipse che dashboard.

## The issues
This is an open project, with the issues listed as github issues.
The code and components:

Component 1: A docker file to create Obeo Designer in a container, with a VNC client (so that it can communicate with Apache guacamole), secured to run as non-privileged user, including any required file directories, permissions or components to allow the successful ‘injection’ of necessary Eclipse Che workspace components/agents, and otherwise limited in its ability.

Component 2: A recipe for the Obeo Designer container  as a Che stack.

Component 3: Apache Guacamole Web Application

Component 4: Apache Guacamole daemon.

## Openshift integration

A lot of work is currently being done to make Che work well with Openshift (Redhat's Kubernetes based PAAS). Rich Lucente's work shows that gaucamole, eclipse RCP applications and openshift can work well together, network end points are easy to find for the eclipse applications container's , and Gaucamole runs well in a openshift/kubernetes pod.
Openshift requires (very sensibly) that containers do not run as priveleged users, Rich Lucente has provided a wrapper for the Guacamole web application running in a docker contianer as a non priveleged user suitable for openshift at rlucentesejboss/guacamole .

## Setup

To set up the demo application using Che, Obeo designer, and Gaucamole, is described here : 

https://github.com/neilmackenzie/visual-che/edit/master/setup.md

## Impacts of Che workspaces on collaborative modelling

One common application of visual tooling  is modelling. Modelling is ussualy done by domian experts, who may be less familiar with technical installation and upkeep of modelling software, and also less familiar with concepts such as git branches, merging and conflict resolution.  Can Che workspaces make collaborating on models easier, we explore the topic here:

https://github.com/neilmackenzie/visual-che/edit/master/collaborative_modelling_with_che.md

## Current status

We have a docker file to create a non-privileged container with Obeo designer and a VNC client, with a ‘/projects’ directory created to be used by eclipse Che, and permissions set.

We have a Che recipe for the Che stack. The recipe includes a dev machine and another machine. It appears that recipes must include a dev machine (which has a set of required che agents)..these che agents will not yet install because of dependencies/requirements in the Obeo designer container that we do not meet yet, this is current priority to fix this. The recipe will load and allow terminal access.

We have not yet integrated the Apache Guacamole Client and deamon into the application, key to doing this will be our approach to determining how we find the address of the started Obeo Designer containers, and how/if we decide to integrate these existing components or just run them in a separate server.





