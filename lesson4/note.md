# Lesson 4

## Agenda

Use hadoop to run below example:

- Wordcount
- Pi
- Secondary Sort

## Steps

### 0. Start docker compose

```bash
docker-compose up -d
```

### 1. login to the hadoop master namenode

use docker exec to login to the namenode container

`exec` command is used to run a command in a running container.

`-it` option is used to open an interactive terminal.

```bash
docker exec -it lesson4_namenode_1 bash
```

### 2. Install curl wget and vim

In container, run below command to install curl, wget and vim

`apache/hadoop` image is based on `redhat` image, so we can use `yum` to install packages.

```bash
sudo yum update && sudo yum install -y curl wget neovim
```

### 3. Get wordcount example data

`curl` command is used to download file from internet.

```bash
curl https://raw.githubusercontent.com/brunoklein99/deep-learning-notes/master/shakespeare.txt -o shakespeare.txt
```

### 4. Check datanode status

`hdfs dfsadmin -report` command is used to check datanode status.

```bash
hdfs dfsadmin -report
```

you will see 4 datanode online.

### 5. Wordcount example

```bash
hadoop fs -mkdir /wordcount
```

```bash
hadoop fs -mkdir /wordcount/input
hadoop fs -mkdir /wordcount/output
```

```bash
hadoop fs -put  ./shakespeare.txt /wordcount/input
```

```bash
yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar wordcount /wordcount/input/shakespeare.txt /wordcount/output/test_out
```

```bash
hadoop fs -cat /wordcount/output/test_out/part-r-00000
```

### 6. Pi

```bash
yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar pi 2 10000
```

### 7. Secondary Sort

```bash
hadoop fs -mkdir -p /s_sort/input
hadoop fs -mkdir -p /s_sort/output
```

```bash
vi s_sort.txt
```

```txt
123,555
2781,2144
1,6
7,2
511,47
32,133
90,11
217,12
12,13
```

```bash
hadoop fs -put  ./s_sort.txt /s_sort/input
```

```bash
yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar secondarysort /s_sort/input/s_sort.txt /s_sort/output/ss
```

```bash
hadoop fs -cat /s_sort/output/ss/part-r-00000
```

### 8. Exit container

```bash
exit
```

## References

- [Hadoop MapReduce Examples](https://hadoop.apache.org/docs/r3.3.6/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html)
