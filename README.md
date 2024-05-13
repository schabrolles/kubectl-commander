# kubectl-commander

This script uses the `fzf` command-line tool to create an interactive menu for selecting and manipulating Kubernetes objects.

When you run this script, it will create an interactive menu that allows you to select one of these options for each object in your Kubernetes cluster. The selected option will be executed on the current object, and any relevant output (e.g., logs or events) will be displayed in a new terminal window.

Conveniant like a gui, quick and responsive like a cli ;)  

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

## Screenshot

Navigate through pods and displaying YAML instantaneously on the right. 
<img width="800" alt="pods_yaml" src="https://github.com/schabrolles/kubectl-commander/assets/19491077/59a7f8ae-130c-47e6-81cd-41cff6d45848">

Quckly display pods Logs (in follow mode).
<img width="800" alt="pods_log" src="https://github.com/schabrolles/kubectl-commander/assets/19491077/9d34a1f1-971a-4013-8590-86c90eadb686">

kube-commander in action:
[![asciicast](https://asciinema.org/a/JRkXUSCQmHRSuLfjAnla47o1p.svg)](https://asciinema.org/a/JRkXUSCQmHRSuLfjAnla47o1p)
  - filter pods
  - [ctrl-y]: view yaml
  - [ctrl-l]: view logs
  - [ctrl-d]: delete pods
  - [ctrl-w]: wtach mode

## Installation

Put the kubctl-commander into a directory that is part of your PATH environement variable. (like /usr/local/bin).

- check the directries part of your PATH
```
echo $PATH
```

- Copy the plugin into the chosen directory and set the execute permission on it.
```
cp kubectl-commander /usr/local/bin
chmod +x /usr/local/bin/kubectl-commander
```

- check if the plugin is available with your kubectl
```
kubectl plugin
```

- (optional) use a symbolic link or alias if you want a shorter name
```
ln -s /usr/local/bin/kubectl-commander /usr/local/bin/kubectl-com
```

### Prerequistes

To enjoy kube commander, please install the 2 following product:
- fzf: https://github.com/junegunn/fzf/releases
- yq:  https://github.com/mikefarah/yq/releases

Uncompress and copy the fzf and yq binaries into your PATH DIR

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
