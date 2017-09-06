## setting up demo

Step 1. Install and run eclipse che

Step 2. Open the Che web application

Step 3. Chose 'stacks' on the left hand panel.

Step 4. chose 'ADD Stack'

Step 5. choose visual che as the stack name

Step 6. Click 'Show' next to the raw configuration section

Step 7. delete any raw configuration, and copy and paste the contents of  https://github.com/neilmackenzie/visual-che/blob/master/visual_che_recipe.txt into the raw configuration. This configurationpoints to the Obeo Designer container on docker hub.

Step 8. delete any tags such as Java 1.8

Step 9. click Save

Step 10. create a new workspace from the eclipse che dashboard, Choose visual-che as the stack

Step 11. you should find you have access to a terminal, showing that the container has been started

Next steps are to access that container in a web browser from Apache Guacamole, this step depends upon some ope issues.
