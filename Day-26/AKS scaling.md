Scaling AKS cluster with cost efficient way. 

##

You will learn how companies like Netflix, HBO, Jio or others scale their Kubernetes clusters to handle millions of users. Alot of people think they do it using Cluster Auto Scaler but the default Cluster Auto scaler does not help them. 

Why ? because the cluster auto scaler takes few minutes to start the node and run the cloud init scripts on the node. Users will see the downtime or slowness during this time which is a bad user experience. 

To solve this problem many customers on AWS add a fleet of nodes at once which will solve their problem but it is not a cost efficient way.
Azure has a solution to this. Cluster Auto Scaler with certain configurations will solve this problem. 

link -->  https://www.youtube.com/watch?v=z2qRGl9hqBU&list=PLdpzxOOAlwvIcxgCUyBHVOcWs0Krjx9xR&index=27

##


![Image](https://github.com/user-attachments/assets/93090304-0328-4a4b-8355-de93f9f9bccf)
