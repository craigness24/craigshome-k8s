# home-assistant
After installation I had an issue not being able to access the app through nginx ingress. Some research resulted in a config that I needed to add into home-assistant configuration.yaml. I edited the configuration.yaml directly using the vscode addon in the browser and then restarted the home-assistant container. 
See the HTTP 400 bad request custom config here:
https://artifacthub.io/packages/helm/k8s-at-home/home-assistant
I also enabled the nginx websocket config from those instructions.

# frigate
Frigate home-assistant integrations recommends using the official integration which requires HACS. 
https://blakeblackshear.github.io/frigate/usage/home-assistant
To install HACS I looked at the install script to see what it was trying to do and then just downloaded the .zip url in my browser and extracted it locally. Then I copied the contents into the home-assistant config/custom_components/hacs directory. After a restart the HACS integration was available to add from the home-assistant UI. The intregation setup was very slow...

I had to restart home-assistant a few times from the configuration -> sever control in th UI and retry the HACS integration to finally install correctly.
