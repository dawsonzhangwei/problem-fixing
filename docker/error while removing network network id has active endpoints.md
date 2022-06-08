Q: error while removing network: <network> id has active endpoints

A: https://stackoverflow.com/questions/70400523/error-while-removing-network-network-id-has-active-endpoints

To list your networks, run docker network ls. You should see your <network> there. Then get the containers still attached to that network with (replacing your network name at the end of the command):

docker network inspect \
  --format '{{range $cid,$v := .Containers}}{{printf "%s: %s\n" $cid $v.Name}}{{end}}' \
  "<network>"
For the various returned container id's, you can check why they haven't stopped (inspecting the logs, making sure they are part of the compose project, etc), or manually stop them if they aren't needed anymore with (replacing the <cid> with your container id):

docker container stop "<cid>"
Then you should be able to stop the compose project.