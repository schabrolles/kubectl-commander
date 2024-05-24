# kubectl-commander

**Unlock Insights into Your Kubernetes Cluster**
Are you tired of digging through logs and events to troubleshoot issues in your Kubernetes cluster? This powerful plugin gives you the tools you need to gain instant insights and control over your objects.

Supercharged by [fzf](https://github.com/junegunn/fzf), it creates an intuitive menu that lets you navigate and dig your kubernetes cluster, select from a range of options for each object - whether it's viewing logs, checking events, or executing custom commands - and watch as the results are displayed into terminal window.

Gain instant visibility into your cluster's performance and behavior with minimal effort. No more tedious searching through logs and events; with this plugin, you'll have everything at your fingertips.

Conveniant like a gui, quick and responsive like a cli ;) 

## Screenshots

Navigate through pods while displaying YAML.|Quckly display pods Logs (in follow mode).
:-----------------------:|:-----------------------:
<img width="800" alt="pods_yaml" src="https://github.com/schabrolles/kubectl-commander/assets/19491077/59a7f8ae-130c-47e6-81cd-41cff6d45848"> | <img width="800" alt="pods_log" src="https://github.com/schabrolles/kubectl-commander/assets/19491077/9d34a1f1-971a-4013-8590-86c90eadb686">

## Quickstart

### Prerequisites

#### krew 
Note: You will need `git` to install the `krew` plugin.
the `commander` plugin is installed using the krew plugin manager for Kubernetes CLI. Installation instructions for krew can be found [here](https://krew.sigs.k8s.io/docs/user-guide/setup/install/).

#### Other needed software
To enjoy kube commander, please install the 2 following product:
- fzf: https://github.com/junegunn/fzf/releases
- yq:  https://github.com/mikefarah/yq/releases

Uncompress and copy the fzf and yq binaries into your PATH DIR

### Installation

After installing & configuring the k8s krew plugin, install outdated using the following command:

```
kubectl krew install commander
```

## Usage

* basic 
```
kubectl commander pods
```
this will open kubectl commander to list all the pods in the current namespace.

* All namespaces
```
kubectl commander pods -A
```

* multiple objects 
```
kubectl commander secret,configmap -A
```

* Don't remember the object name ?
```
kubectl commander -a
```
=> This will open an fzf list of all the objects installed on your cluster. Enter a fzf query, select the objects you want (with TAB) then press Enter. 

## Key Bindings:

| key Binding     | Actions                                                        |
|-----------------|----------------------------------------------------------------|
| ctrl-h          | print this help menu                                           |
| ctrl-q          | Quit                                                           |
| ctrl-r          | Reload                                                         |
| TAB             | select items                                                   |
| ctrl-a          | select all items                                               |
| ctrl-alt-a      | deselect all items                                             |
| ctrl-y          | preview YAML.<br>* press this key several time to cycle between preview mode (right,top,hidden)<br>* press 'Enter' to add/change the yq query (default is '.') .           |
| ctrl-v          | preview and follow Events (for objects which have events)<br>* press this key several time to cycle between preview mode (top 50%,top 80%,hidden)<br>* press 'Enter' to follow the events in full screen |
| ctrl-l          | preview and follow Logs (for pods)<br>* press this key several time to cycle between preview mode (top 50%,top 80%,hidden)<br>* press 'Enter' to follow the events in full screen            |
| ctrl-x          | Enter into container (for pods, deployments)                   |
| ctrl-d          | /!\ delete object /!\ (works with multi selection)             |
| ctrl-e          | edit object                                                    |
| ctrl-s          | edit secret (decrypt/encrypt)<br>-> (need 'modify-secret' krew plugin)|
| ctrl-w          | toggle watch mode (automatic refresh 2s)                       |
| alt-l           | toggle wrap line in preview (default off)                      |

kube-commander in action:
[![asciicast](https://asciinema.org/a/JRkXUSCQmHRSuLfjAnla47o1p.svg)](https://asciinema.org/a/JRkXUSCQmHRSuLfjAnla47o1p)
  - filter pods
  - [ctrl-y]: view yaml
  - [ctrl-l]: view logs
  - [ctrl-d]: delete pods
  - [ctrl-w]: wtach mode

