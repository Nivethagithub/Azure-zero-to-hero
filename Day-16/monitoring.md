To have the effictive monitoring system, we have to implement all the key metrics, not just CPU/memory utilizations tracking. 

level monitoring system 1 :  Network components, issues     : Tools  --> Network Watcher 
level monitoring system  2 :  Nodes (Clusters, VMss) issues   : Tools  --> prometheus (In azure they have managed prometheus service, we can create custom metrics) 
level monitoring system  3 : control plane ( etcd, sheduler ...etc)  : Tools  -->  Azure monitor  (Container insights)
level monitoring system  4 :  Pods, container   : Tools  --> prometheus 
level monitoring system  5 : APM, application performance : Tools  --> Application insights
level monitoring system  6 : VM, storage accounts :   Tools  -->  Azure monitor

For visualization --> use grafana


