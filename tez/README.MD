# Apache Tez

This initialization action installs the latest version of [Apache Tez](https://tez.apache.org/) on a [Google Cloud Dataproc](https://cloud.google.com/dataproc) cluster. In this initialization action:

1. Required libraries such as [`protobuf`](https://github.com/google/protobuf) are installed
2. Tez is compiled
3. Tez is put into HDFS
4. Hadoop and Hive are configured to work with Tez on the Dataproc cluster

## Using this initialization action
You can use this initialization action to create a new Dataproc cluster with Apache Tez installed:

1. Use the `gcloud` command to create a new cluster with this initialization action. The following command will create a new cluster named `<CLUSTER_NAME>`.

    ```bash
    gcloud dataproc clusters create <CLUSTER_NAME> \
      --initialization-actions gs://dataproc-initialization-actions/tez/tez.sh
    ```
1. Once the cluster is created, Tez should work with your Cloud Dataproc jobs.

1. Hive should be configured to use Tez, rather than Mapreduce, as its execution engine. This can significantly speed up some Hive queries. Read more in the [Hive on Tez documentation](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez).

You can find more information about using initialization actions with Dataproc in the [Dataproc documentation](https://cloud.google.com/dataproc/init-actions).

## Important notes

* This script has a number of user-defined variables at the top, such as the Tez version and install location.
* This script builds from source which may cause issues if you use an unstable release.
* Be careful with the [`protobuf`](https://github.com/google/protobuf) version - Tez often requires a *very specific* version to function properly.
