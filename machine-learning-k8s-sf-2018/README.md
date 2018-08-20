Machine learning on k8s
=======================

This are the files used in the for my talk on [Machine learning on k8s](https://www.meetup.com/San-Francisco-Kubernetes-Meetup/events/253147136/). The slides are posted [here](https://speakerdeck.com/dharmeshkakadia/machine-learning-on-kubernetes).

Resources:

- [jupyter-dev.yaml](#jupyter-dev.yaml) is an example pod spec that you can use to get a working data science notebook on kubernetes.
- [Dockerfile](#Dockerfile) is an example Dockerfile to customize the notebook image.
- [demo.ipynb](#demo.ipynb) is as notebook showing end-to-end ML example.
- [training.yaml](#training.yaml) is an example of creating a training pipeline to train the models daily as kubernetes cronjobs.

## Get data science Juypter notebook with GPU and data locally available

After creating k8s secrets corresponding to your environment and/or editing the [jupyter-dev.yaml](#jupyter-dev.yaml) suitably, you can run the following to create a jupyter pod.

```
kubectl apply -f jupyter-dev.yaml
```

Run the local proxy to get access the pod
```
kubectl port-forward jupyter-dev 8888:8888
```

Run the following to get access token/URL :

```
kubectl exec -it jupyter-dev jupyter notebook list
```

This would give output similar to below, which you can click to get access to the Juypter notebook with data and GPUs.
```
Currently running servers:
http://localhost:8888/?token=eeb9cc37b6fb36318226b3b7345aea65c7080dd2d526813b :: /code
```

You can get access to bash terminal if you like bash interface directly (for running grep etc on your data). Of course you can run bash commands and access terminal within jupyter as well.
```
kubectl exec -it jupyter-dev bash
```

## End to End Machine learning example

[demo.ipynb](#demo.ipynb) is an augmented example from Tensorflow that shows GPU and mounted data access with end-to-end fashion MNIST dataset. You can import it by clicking `upload` button in your jupyter and importing `demo.ipynb`.

## Blobfuse

Blobfuse makes Azure Blobs available as mounted local path, with configurable caching. Follow [Blobfuse documentation](https://github.com/Azure/kubernetes-volume-drivers/tree/master/flexvolume/blobfuse) for working with it.
