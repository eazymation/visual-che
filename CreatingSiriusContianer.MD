## Sirius Container build
We have already built  the Sirius container image and stored it in dockerhub.
It downloaded and used the Obeo Designer 10 install.
Also in that container we have added bundles to allow the user to easily use
the  example family model. Note that to do this we created an eclipse update site,
which is stored as the directory. 
https://github.com/neilmackenzie/visual-che/tree/master/resources/family_updatesite
 this update site is installed automatically before the user has access to the application.

To create that update site we followed the instructions here:
https://www.eclipse.org/forums/index.php/t/1076701/

You can see how this container is built by looking at the docker file in this repository.
We reference this from dockerhub which builds and stores the container:
https://hub.docker.com/r/neilmackenzie/visual-che/
