# Deploying nginx pods and accessing apps

This exercise is meant to show the usage of deploying something on the pod and then further accessing it using a service called **nodeport**.

Note that I have used the default nextjs app instead of nginx in this example to keep it more practical.

Do not that nodeport will map the pods exposed port to `http://node_IP:nodePort` which essentially is a field you give in the yaml file or else a random value from 30000 to 32707 is picked up.